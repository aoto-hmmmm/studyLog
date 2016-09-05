# 关于在VPS中架设SS(libev)
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
```

##关于运行ss服务
```bash
ss-server [option]
/etc/init.d/shadowsocks-libev [start-status-stop-...]
#修改默认启动文件后推荐使用这一种
service shadowsocks-libev [start-status-stop-...]
```
