# Linux

## 教程

[鳥哥的 Linux 私房菜 -- 鳥哥的 Linux 私房菜 首頁](http://linux.vbird.org/)

[Linux基础 — Linux Tools Quick Tutorial](http://linuxtools-rst.readthedocs.io/zh_CN/latest/base/index.html)

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
[Linux递归删除文件命令](http://bbs.csdn.net/topics/380267110)**【危险操作】**

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

### wget

#### wget 批量下载 Apache directory listing 列目录

```
wget -m -np https://featherbear.github.io/UNSW-COMP6441/blog/
```

[apache directory listing, download all](https://stackoverflow.com/a/5317668)


#### 使用 Wget 镜像下载受限网站

**概述**
当网站需要通过特定代理服务器访问且必须登录时，常规下载工具通常无法奏效。可通过使用 `wget` 命令行工具，在这些限制条件下递归下载完整网站（制作镜像）以供离线浏览。


```bash
wget -r -p -np -k \
     -e use_proxy=yes \
     -e http_proxy=192.168.238.88:8118 \
     --header="Cookie: 你的_COOKIE_字符串" \
     http://www.yourwebsite.com/
```

**参数详解**
1.  **结构与资源 (`-r`, `-p`)**：开启递归下载（自动跟随链接）并抓取页面显示所需的所有附属资源（图片、CSS、JS），确保本地浏览时排版正常。
2.  **范围控制 (`-np`)**：意为 "No Parent"（不追溯父级）。它强制 `wget` 仅下载当前目录及子目录的内容，防止误下载到上级不需要的文件夹。
3.  **离线兼容 (`-k`)**：下载完成后，自动将 HTML 中的链接修改为“相对路径”。这使得您在没有网络连接时，依然可以双击打开网页并正常跳转。
4.  **代理配置 (`-e`)**：显式指令 `wget` 将所有网络流量路由至指定的代理服务器 (`192.168.238.88:8118`)。
5.  **身份验证 (`--header`)**：通过在请求头中伪造 Cookie，将您的登录状态传递给服务器，从而绕过登录拦截。


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


[Adopt a good cause, DON'T SIGKILL](http://turnoff.us/geek/dont-sigkill-2/)