# Trackpoint 小红点


[https://askubuntu.com/questions/37824/what-is-the-best-way-to-configure-a-thinkpads-trackpoint](https://askubuntu.com/questions/37824/what-is-the-best-way-to-configure-a-thinkpads-trackpoint)

`/etc/udev/rules.d/10-trackpoint.rules`


```
SUBSYSTEM=="serio", DRIVERS=="psmouse", DEVPATH=="/sys/devices/platform/i8042/serio1/serio2", ATTR{sensitivity}="160", ATTR{speed}="40" 
```
