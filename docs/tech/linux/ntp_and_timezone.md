# Ntp and Timezone 时间和时区

In Linux, there are two main options: `ntpd` and `systemd-timesyncd`。

### ntpd (Network Time Protocol Daemon):

1. **Accuracy and Precision**:
   - **ntpd**: NTP is known for its high accuracy and precision in time synchronization. It adjusts the system clock gradually to minimize abrupt changes.
  
2. **Complexity**:
   - **ntpd**: ntpd is more complex and feature-rich compared to timesyncd. It provides advanced configuration options and is suitable for servers that require highly accurate time synchronization.

3. **Stratum**:
   - **ntpd**: ntpd can act as both a client and a server in the NTP hierarchy. It can operate at various stratum levels, allowing for more flexibility in network time synchronization.

4. **Use Case**:
   - **ntpd**: ntpd is commonly used in server environments where precise time synchronization is crucial, such as financial institutions, data centers, and scientific research facilities.

### [Recommended]systemd-timesyncd:

1. **Simplicity**:
   - **timesyncd**: systemd-timesyncd is a simpler and lightweight alternative to ntpd. It is part of the systemd suite and is designed for basic time synchronization needs.

2. **Automatic Configuration**:
   - **timesyncd**: timesyncd is easier to set up and requires minimal configuration. It automatically selects and synchronizes with time servers specified in systemd's configuration.

3. **Systemd Integration**:
   - **timesyncd**: timesyncd integrates well with systemd and is the default time synchronization solution on many modern Linux distributions.

4. **Use Case**:
   - **timesyncd**: timesyncd is suitable for desktops, laptops, and systems where high precision time synchronization is not critical. It provides accurate timekeeping for most everyday use cases.


If you do not need to setup the NTP server, choose `systemd-timesyncd`.

## systemd-timesyncd 时钟同步

Timesyncd is a lighter-weight alternative to ntpd that is more integrated with systemd. However, that it doesn’t support running as a time server.

Timesyncd is the built-in tool to replace ntpd in Debian.

Get current time:

```shell
date
```

## sync time using Timesyncd

Check if timesyncd is running:

```shell
sudo systemctl status systemd-timesyncd
```

Setup the ntp server:

```shell
sudo nano /etc/systemd/timesyncd.conf
```

```conf
[Time]
NTP=10.243.80.254 # Your NTP server here
FallbackNTP=10.243.80.86 10.243.80.87 10.243.80.251 # Alternative NTP server
#FallbackNTP=0.debian.pool.ntp.org 1.debian.pool.ntp.org 2.debian.pool.ntp.org 3.debian.pool.ntp.org
RootDistanceMaxSec=60
PollIntervalMinSec=32
PollIntervalMaxSec=2048
ConnectionRetrySec=30
SaveIntervalSec=60
```

Restart the service:

```shell
sudo systemctl restart systemd-timesyncd
```

Should return this:

```shell
● systemd-timesyncd.service - Network Time Synchronization
     Loaded: loaded (/lib/systemd/system/systemd-timesyncd.service; enabled; preset: enabled)
     Active: active (running) since Wed 2024-05-15 10:52:32 CST; 22min ago
       Docs: man:systemd-timesyncd.service(8)
   Main PID: 28770 (systemd-timesyn)
     Status: "Contacted time server 10.243.80.254:123 (10.243.80.254)."
      Tasks: 2 (limit: 19094)
     Memory: 1.5M
        CPU: 57ms
     CGroup: /system.slice/systemd-timesyncd.service
             └─28770 /lib/systemd/systemd-timesyncd

May 15 10:52:32 debian-server systemd[1]: Starting systemd-timesyncd.service - Network Time Synchronization...
May 15 10:52:32 debian-server systemd[1]: Started systemd-timesyncd.service - Network Time Synchronization.
May 15 11:01:48 debian-server systemd-timesyncd[28770]: Contacted time server 10.243.80.254:123 (10.243.80.254).
May 15 11:01:48 debian-server systemd-timesyncd[28770]: Initial clock synchronization to Wed 2024-05-15 11:01:48.856403 CST.

```

If you got this 'Server has too large root distance. Disconnecting.' error, it means that the time difference between your system and the time server you are trying to sync with is [too large][1]. You need to change the `RootDistanceMaxSec` larger.

[1]: https://unix.stackexchange.com/questions/655488/synchronizing-ntp-machines-with-a-high-root-time-server


## links

- https://manpages.debian.org/bookworm/systemd-timesyncd/systemd-timesyncd.8.en.html
- http://www.jinbuguo.com/systemd/systemd-timesyncd.service.html


## ntpd 时间同步

通过NTP服务器修正：

安装`ntpdate`:
```
sudo apt install ntpdate
```
使用中国的NTP服务器:
需要保证ntp服务**不在**运行。
```
sudo ntpdate cn.pool.ntp.org
```

启用NTP服务：
```
sudo apt install ntp
sudo service ntp start
```

## tzselect 设置时区

命令行工具`tzselect`可以设置时区，说白了就是执行以下步骤（修改为北京时间）：

```
cat >>~/.profile<<EOF
TZ='Asia/Shanghai'; export TZ
EOF
```
重新开始用户会话（重连SSH）生效。

## Find NTP server on local network

Use `nmap` to search for available NTP servers on your local network:

```shell
nmap -p 123 --script ntp-info 192.168.1.0/24
```

This command will scan the specified IP range for devices with port 123 (the default port for NTP). The `--script ntp-info` option tells nmap to run the NTP script, which will help identify NTP servers.