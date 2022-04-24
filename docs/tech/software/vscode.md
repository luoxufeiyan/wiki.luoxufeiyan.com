# VS Code

## Remote SSH 使用代理

如果 Remote SSH 希望使用代理连接，可以修改 `~/.ssh/config` 文件，增加下面一行。

```shell
ProxyCommand "C:\Program Files\Git\mingw64\bin\connect.exe" -H 127.0.0.1:1080 %h %p
```

PS： Windows为例，且已经安装了 Git，其他方法请参考 [Jump-Box](https://code.visualstudio.com/blogs/2019/10/03/remote-ssh-tips-and-tricks#_proxycommand)

```shell
Host badscrew_web
  User badscrew
  Port 22
  Hostname 123.123.123.123
  IdentityFile "c:\Users\badscrew\mykeys\ssh\id_rsa"
  TCPKeepAlive yes
  IdentitiesOnly yes
  ProxyCommand "C:\Program Files\Git\mingw64\bin\connect.exe" -H 127.0.0.1:1080 %h %p
```

ref: https://github.com/microsoft/vscode-remote-release/issues/117#issuecomment-547496229
