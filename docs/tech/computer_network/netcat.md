# netcat

* `-l` listen
* `-u` udp 
* `-4` IPv4 only

向端口发送数据: ` echo "hi"|nc -4u -w0 localhost 5000`

监听端口: `nc -lu localhost 5000`

## 主机之间复制文件

接收文件： `nc -l 5000 > my.jpg`

发送文件：`nc HOST-IP 5000 < my.jpg`