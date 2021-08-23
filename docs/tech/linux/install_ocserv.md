# 安装ocserv

脚本：[[https://github.com/fanyueciyuan/eazy-for-ss/tree/master/ocservauto|eazy-for-ss/ocservauto at master · fanyueciyuan/eazy-for-ss · GitHub]]

教程：[[https://www.fanyueciyuan.info/fq/ocserv-debian.html|OpenConnect server(ocserv)  一键脚本 for deibian 7+  - 翻跃 瓷院]]

注意需要对防火墙做masquerade：

```
#!/bin/bash
sysctl -w net.ipv4.ip_forward=1 > /dev/null 2>&1
gw_intf_oc=`ip route show|sed -n 's/^default.* dev \([^ ]*\).*/\1/p'`
iptables -t nat -A POSTROUTING -s 192.168.10.0/24 -o $gw_intf_oc  -j MASQUERADE
iptables -A FORWARD -s 192.168.10.0/24 -j ACCEPT
iptables -A INPUT -p tcp --dport 999 -j ACCEPT
iptables -A INPUT -p udp --dport 20 -j ACCEPT
iptables -A FORWARD  -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -t mangle -A FORWARD -p tcp -m tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu
```

## 客户端

### Linux

```
sudo apt install openconnect
```

CLI，root权限执行。

### Android
OpenConnect