# 桌面程序创建.desktop文件

## 文件路径

当前用户：`~/.local/share/applications`

全局：`/usr/share/applications/`

## 文件内容
以OBS为例：
```
[Desktop Entry]
Version=1.0
Name=OBS
GenericName=Streaming/Recording Software
Comment=Free and Open Source Streaming/Recording Software
Comment[ru]=Бесплатная программа с открытым кодом для записи/трансляции видео
Exec=obs
Icon=obs
Terminal=false
Type=Application
Categories=AudioVideo;Recorder;
StartupNotify=true
```

Exec为启动命令。

[How to Create a .Desktop File For Your Application in Linux - Make Tech Easier](https://www.maketecheasier.com/create-desktop-file-linux/)