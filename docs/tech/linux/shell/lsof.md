# lsof 命令

List of files 查看系统文件。

## 一切皆文件

### 查找某个文件相关的进程
```
$ lsof /bin/bash
COMMAND     PID USER  FD   TYPE DEVICE SIZE/OFF    NODE NAME
mysqld_sa  2169 root txt    REG  253,0   938736 4587562 /bin/bash
ksmtuned   2334 root txt    REG  253,0   938736 4587562 /bin/bash
bash      20121 root txt    REG  253,0   938736 4587562 /bin/bash
```

### 哪些程序在使用端口
```
$ lsof -i :1081
COMMAND     PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
dropbox    2870  gao   37u  IPv4  33241      0t0  TCP localhost:44090->localhost:1081 (CLOSE_WAIT)
chrome     4224  gao  136u  IPv4 778700      0t0  TCP localhost:58924->localhost:1081 (ESTABLISHED)
Telegram   6611  gao   27u  IPv4 784936      0t0  TCP localhost:59208->localhost:1081 (ESTABLISHED)
```

[外部链接](http://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/lsof.html)