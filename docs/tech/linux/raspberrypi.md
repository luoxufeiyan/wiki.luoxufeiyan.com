# 树莓派

## 换源
树莓派使用的Raspbian发行版与Debian软件源不同，但发型代号及版本与Debian保持一致。

替换为USTC镜像源

编辑/etc/apt/sources.list文件。注释掉原内容，添加下面两行：
```
deb http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main non-free contrib
deb-src http://mirrors.ustc.edu.cn/raspbian/raspbian/ stretch main non-free contrib
```
随后`sudo apt update`更新。

[Raspbian镜像使用帮助 [LUG@USTC](https://lug.ustc.edu.cn/wiki/mirrors/help/raspbian)]

## 解决树莓派SSH提示Connection reset的问题

新版的Raspbian系统默认不开启SSH，需要在boot分区内新建一个名为`ssh`的文件方可开启SSH。

不过我不仅添加了这个文件，也直接在树莓派中手动编辑了`/etc/ssh/sshd_config`文件，启动了SSH服务。但SSH连接仍然提示Connection reset。


通过`ssh -vvv pi@192.168.2.3`排查，SSH服务已经启动，但存在废弃的SSH秘钥。

解决方法：
```
sudo rm /etc/ssh/ssh_host_* 
sudo dpkg-reconfigure openssh-server
```
删除SSH秘钥，重新配置SSH服务。

[树莓派 Connection reset by *.*.*.* port 22](http://qinfei.glrsmart.com/2017/08/14/s/)

## 吃灰？
  * HomeBridge
  * aria2
  * ~~MediaTomb~~ 不是很好用，还是miniDLNA吧。
  * DHT11房间温度监控
  * gammu手机短信转发
  * [智能花盆](http://www.instructables.com/id/Plantbot-Beta/)
  * [更多DIY](https://www.adafruit.com/)