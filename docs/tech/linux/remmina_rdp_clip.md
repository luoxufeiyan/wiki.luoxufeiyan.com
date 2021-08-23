# 解决Remmina不能与Windows共享剪贴板的问题

首先确定Remmina设置里**没有勾选**“禁用剪贴板同步”（默认未选中）。

![](remmina-pastebin-sync.png)

出现这个问题一般是Windows的`rdpclip.exe`挂了，直接在任务管理器中杀死`rdpclip.exe`，随后重新启动即可。记得重启之后重连一下Remmina。

