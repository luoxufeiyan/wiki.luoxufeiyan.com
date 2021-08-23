# nmap 扫描工具

## 扫描内网段在线主机
```
nmap -sP 192.168.24.*
```

## 扫描主机开放端口
```
nmap -A 27.212.43.97
```

## 扫描主机操作系统
```
 nmap -O 172.16.0.221
```
```
Starting Nmap 6.47 ( http://nmap.org ) at 2018-02-22 17:01 CST
Nmap scan report for 172.16.0.221
Host is up (0.0048s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
MAC Address: 00:16:3E:FC:97:D3 (Xensource)
Device type: general purpose
Running: Linux 3.X
OS CPE: cpe:/o:linux:linux_kernel:3
OS details: Linux 3.11 - 3.14
Network Distance: 1 hop

OS detection performed. Please report any incorrect results at http://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 91.10 seconds
```