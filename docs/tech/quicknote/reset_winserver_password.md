# 重置WinServer密码

步骤
```
1在虚拟机的光盘中选择原操作系统的ISO，并确定（如果是物理机，直接把ISO刻录成光盘，放入光驱即可）
2重启服务器，修改启动项从CD-ROM启动，当在屏幕出现Press any key to boot from CD or DVD字样时，马上按任意键进入光盘引导模式，根据提示，选择下一步
3在光盘引导的系统安装界面，选择修复计算机
4在弹出的系统恢复选项中，选择使用可以帮助解决Windows 启动问题的恢复工具，并选择要修复的操作系统
在系统恢复选项中，选择恢复工具为命令提示符。然后进行如下几步操作：
1）在弹出的命令提示符中，切换到系统分区，输入d: （为第3步中显示的盘符）。
2）输入D:\>copy  d:\windows\system32\osk.exe d:\ 命令来备份osk.exe(这个程序是轻松访问中的屏幕键盘，可以在登陆界面调用)。
3）输入D:\>del  d:\windows\system32\osk.exe 命令来删除原来的osk.exe文件。
4）输入D:\>rename d:\windows\system32\cmd.exe osk.exe 命令把cmd.exe重命名为osk.exe，然后重启系统。
5系统重启过程中，本次不要从光盘引导，而从硬盘进行引导，在系统登录界面，点击轻松访问按钮，在弹出的轻松访问对话框中，勾选屏幕键盘，然后确定。
6弹出的屏幕键盘程序，其实是CMD命令界面（因为前面我们把osk.exe替换为cmd.exe了）。
              1）查看系统下的用户，输入命令：net user；
              2）重置adminitrator用户密码为123456@p，输入命令：net user administrator 123456@p，（一定要是一个包含特殊符号数字字母的复杂密码，且位数超过8位）然后关掉命令窗口

7.按Ctrl+Alt+Del，输入刚才的用户名administrator，并使用重置的秘码123456@p登陆。成功进入系统后。
8.需要恢复替换的文件，（系统变得会不安全）。恢复的方法：
1）重启系统从光盘引导，进入系统恢复选项中的命令提示符
2）输入命令D:\>rename d:\windows\system32\osk.exe cmd.exe 恢复cmd.exe
3）输入命令D:\>copy d:\osk.exe d:\windows\system32\  恢复osk.exe
4）然后重启，才算安全的完成了密码重置（不要忘记把光盘卸载）。
```

[[https://social.technet.microsoft.com/Forums/ie/en-US/62e5d7f5-3639-43d2-8555-7339b6abf4a8/windows-server-2012-r2?forum=winserver8zhcn|windows server 2012 R2登录密码忘了怎么办呢？]]