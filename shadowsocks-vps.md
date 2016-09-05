# 关于在VPS中架设SS所学到的相关知识(libev)
---------

##安装shadowsocks-libev
https://github.com/shadowsocks/shadowsocks-libev

##修改/etc/default/shadowsocks-libev可更改默认启动服务用户
```bash
# Extra command line arguments
#-u开启udp转发 -A开启一次性认证
DAEMON_ARGS="-u -A"

# User and group to run the server as
USER=YOURUSER
GROUP=YOURGROUP

# Number of maximum file descriptors
#最大打开文件数
MAXFD=8000
```

##查看进程与端口情况
```bash
#进程
ps -ef | grep ss-server
#端口
netstat -ap | grep ss-server
```

##关于运行ss服务
```bash
ss-server [option]
/etc/init.d/shadowsocks-libev [start-status-stop-...]
#修改默认启动文件后推荐使用这一种
service shadowsocks-libev [start-status-stop-...]
```

##由于libev不支持多实例配置，所以需要监听多个端口时，可以启用多个ss监听不同端口
首先，制定多个配置文件,L例如：
```bash
cd /etc/shadowsocks-libev
cp ./config.json ./config-test.json
```
更改config-test.json之后，在/etc/default/shadowsocks-libev中增加变量(我这里是CONFFILE_TEST)
```bash
# Configuration file
CONFFILE="/etc/shadowsocks-libev/config.json"
CONFFILE_TEST="/etc/shadowsocks-libev/config-test.json"
```
接下来需要在启动脚本里加入启动代码
第一段
```bash
do_start()
{
    # Modify the file descriptor limit
    ulimit -n ${MAXFD}

    # Take care of pidfile permissions
    mkdir /var/run/$NAME 2>/dev/null || true
    chown "$USER:$GROUP" /var/run/$NAME

    # Return
    #   0 if daemon has been started
    #   1 if daemon was already running
    #   2 if daemon could not be started
    start-stop-daemon --start --quiet --pidfile $PIDFILE --chuid root:$GROUP --exec $DAEMON --test > /dev/null \
        || return 1
    start-stop-daemon --start --quiet --pidfile $PIDFILE --chuid root:$GROUP --exec $DAEMON -- \
        -c "$CONFFILE" -a "$USER" -u -f $PIDFILE $DAEMON_ARGS \
        || return 2
    #新增启动代码，注意$PIDFILE必须换一个，不然会与上面一条命令冲突，
    start-stop-daemon --start --quiet --pidfile ${PIDFILE}-test --chuid root:$GROUP --exec $DAEMON -- \
        -c "$CONFFILE_TEST" -a "$USER" -u -f ${PIDFILE}-test $DAEMON_ARGS \
        || return 2
}
```
第二段
```bash
do_stop()
{
    # Return
    #   0 if daemon has been stopped
    #   1 if daemon was already stopped
    #   2 if daemon could not be stopped
    #   other if a failure occurred
    start-stop-daemon --stop --quiet --retry=KILL/5 --pidfile $PIDFILE --exec $DAEMON
    RETVAL="$?"
    [ "$RETVAL" = 2 ] && return 2
    # Wait for children to finish too if this is a daemon that forks
    # and if the daemon is only ever run from this initscript.
    # If the above conditions are not satisfied then add some other code
    # that waits for the process to drop all resources that could be
    # needed by services started subsequently.  A last resort is to
    # sleep for some time.
    start-stop-daemon --stop --quiet --oknodo --retry=KILL/5 --exec $DAEMON
    [ "$?" = 2 ] && return 2
    # Many daemons don't delete their pidfiles when they exit.
    rm -f $PIDFILE
    
    #新增停止代码,注意$PIDFILE变量改为与上面一致
    start-stop-daemon --stop --quiet --retry=KILL/5 --pidfile ${PIDFILE}-test --exec $DAEMON
    RETVAL="$?"
    [ "$RETVAL" = 2 ] && return 2
    
    start-stop-daemon --stop --quiet --oknodo --retry=KILL/5 --exec $DAEMON
    [ "$?" = 2 ] && return 2
    
    rm -f ${PIDFILE}-test
    #至此
    
    return "$RETVAL"
}
```
改完之后即可用service命令一同管理
