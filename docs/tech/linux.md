# Linux

## 教程

[[http://linux.vbird.org/|鳥哥的 Linux 私房菜 -- 鳥哥的 Linux 私房菜 首頁]]

[[http://linuxtools-rst.readthedocs.io/zh_CN/latest/base/index.html|Linux基础 — Linux Tools Quick Tutorial]]

## 一些Linux命令


### 查找文件体积前10 的文件
```
du -a / | sort -n -r | head -n 10
```

### 生成指定体积文件
```
dd if=/dev/zero of=test1g.bin bs=1M count=1024
```
从零源生成一个1G大小的文件，每次读写1MB，读写1024次。

### 递归删除特定后缀的文件 
[[http://bbs.csdn.net/topics/380267110|Linux递归删除文件命令]]**【危险操作】**

```
find . -name "*.c" -exec rm {} \;
```

### 查看中国分配了多少IP

```
curl https://ftp.apnic.net/stats/apnic/delegated-apnic-extended-latest | grep CN | grep ipv4 | awk -F\| '{print $5}' | paste -sd+ | bc
```

330718720

### 小内存云主机精简系统

128MB内存
```
apt-get -y purge apache2-* bind9-* xinetd samba-* nscd-* portmap sendmail-* sasl2-bin lynx memtester unixodbc odbcinst-* sudo tcpdump ttf-* && apt-get -y autoremove && apt-get -y clean && apt-get update
```
### wget 批量下载 Apache directory listing 列目录

```
wget -m -np https://featherbear.github.io/UNSW-COMP6441/blog/
```

[apache directory listing, download all](https://stackoverflow.com/a/5317668)

## 小抄速记

### 创建备份

```
cp -p /etc/apt/sources.list{,.back} 
```


## 公益广告
```
系统一声吼，进程两行泪
        ——乌邦图企鹅保护协会（宣）
```

![](http://turnoff.us/image/en/dont-sigkill-2.png)


[[http://turnoff.us/geek/dont-sigkill-2/|Adopt a good cause, DON'T SIGKILL]]