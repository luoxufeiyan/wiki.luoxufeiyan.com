# HiDPI高分屏缩放问题

based on Linux mint 19.2

## add custom resolution

make and edit `nano ~/.xprofile`

```
#!/bin/sh
# 2k display
xrandr --newmode "2560x1440_60.00"  312.25  2560 2752 3024 3488  1440 1443 1448 1493 -hsync +vsync
xrandr --addmode DP-1 "2560x1440_60.00
```

## 1.5x scaling

run following command

```
dconf write /org/cinnamon/desktop/interface/scaling-factor 'uint32 2'
dconf write /org/gnome/desktop/interface/scaling-factor 'uint32 2'
dconf write /org/cinnamon/active-display-scale 1.5
```

## 还原1.0缩放

0 为 auto，1 为 1.0x。

```
dconf write /org/cinnamon/desktop/interface/scaling-factor 'uint32 1'
dconf write /org/gnome/desktop/interface/scaling-factor 'uint32 1'
dconf write /org/cinnamon/active-display-scale 1
```

部分Qt程序的缩放可以手动设置`export QT_AUTO_SCREEN_SCALE_FACTOR=0`，写在`~/.bashrc` 中。
```
# Change window scaling for Qt-based programs 
export QT_AUTO_SCREEN_SCALE_FACTOR=0
export QT_SCALE_FACTOR=1

```
[Scaling/HiDPI issue for QT5 applications under GNOME](https://unix.stackexchange.com/questions/433385/scaling-hidpi-issue-for-qt5-applications-under-gnome)