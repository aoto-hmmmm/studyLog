#2016.9.7
##将VPS rebuild之后，SSH连接显示
> WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!

发现是密匙问题，需要在SSH客户端上删掉记录就行了，可问题是自己使用的是chrome下的应用Secure shell,目录结构找到也没有类似的密匙记录文件，
没办法，最后翻官方FAQ找到如何清除:
https://chromium.googlesource.com/apps/libapps/+/master/nassh/doc/FAQ.md#How-do-I-remove-a-known-host-fingerprint-aka-known_hosts_entry

##写bash脚本的时候，如果想要在匹配行插入数据，可以用以下语句
```bash
#行前加
sed -i '/search message/i\insert message' the.conf.file
#行前后
sed -i '/search message/a\insert message' the.conf.file
```

##将变量A的值转为大写并赋予给B
```bash
$B=$(echo $A | tr [a-z] [A-Z])
```
