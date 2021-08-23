## VPS安装ZeroNet

### indipendence
```
sudo apt-get update
sudo apt-get install msgpack-python python-gevent wget
```

### install ZeroNet
```
cd ~
wget https://github.com/HelloZeroNet/ZeroNet/archive/master.tar.gz
tar xvpfz master.tar.gz
mv ZeroNet-master/ ZeroNet/ & rm master.tar.gz
sleep 1s
```

### enable webUI
```
cd ZeroNet/plugins/
mv disabled-UiPassword/ UiPassword/
```

### set firewall
```
ufw allow 33789 43110
```

### run ZeroNet
```
python zeronet.py --ui_ip "*" --ui_password mypasswd
国内运行(for China user)：python zeronet.py --proxy 127.0.0.1:9050 --disable_udp
```

### (optional) run ZeroNet as a daemon:
supervisor
```
[program:ZeroNet]
user=alls
directory=/alls/ZeroNet
command=python zeronet.py --ui_ip "*" --ui_password "mypasswd"
process_name=%(program_name)s
autostart=true
redirect_stderr=true
stdout_logfile=/var/log/ZeroNet.log
stdout_logfile_maxbytes=1MB
stdout_logfile_backups=0
```