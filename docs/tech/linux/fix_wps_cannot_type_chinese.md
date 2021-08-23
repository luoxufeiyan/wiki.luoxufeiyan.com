# 解决WPS 无法输入中文的问题

问题原因是WPS没有正确设置fcitx的环境变量，需要手动添加。

依次编辑/usr/bin目录下wps、wpp、et三个文件。

```
sudo vi /usr/bin/wps
```
分别在第二行添加如下代码：
```
export XMODIFIERS="@im=fcitx"  #自行添加，使能够输入中文
export QT_IM_MODULE="fcitx"  #同上
```
启动WPS即可。