#2016.9.7
将VPS rebuild之后，SSH连接显示
> WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
发现是密匙问题，需要在SSH客户端上删掉记录就行了，可问题是自己使用的是chrome下的应用Secure shell,目录结构找到也没有类似的密匙记录文件，
没办法，最后翻官方FAQ找到如何清除:
https://chromium.googlesource.com/apps/libapps/+/master/nassh/doc/FAQ.md#How-do-I-remove-a-known-host-fingerprint-aka-known_hosts_entry
