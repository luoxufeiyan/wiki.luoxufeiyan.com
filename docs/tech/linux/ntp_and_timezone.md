# 时间和时区

## (推荐) systemd-timesyncd 时间修正 

http://www.jinbuguo.com/systemd/systemd-timesyncd.service.html

## ntpd时间修正

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

## 设置时区

命令行工具`tzselect`可以设置时区，说白了就是执行以下步骤（修改为北京时间）：

```
cat >>~/.profile<<EOF
TZ='Asia/Shanghai'; export TZ
EOF
```
重新开始用户会话（重连SSH）生效。
