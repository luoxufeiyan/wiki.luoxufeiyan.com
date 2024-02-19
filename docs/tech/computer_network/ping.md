# ping

使用带源 IP 的 ping，例如从 source IP ping 到 target IP:

Windows 下：

```cmd
ping [target address](x.x.x.x) -S [source address](x.x.x.x)
```

Linux 下：

```bash
ping -I [source address](x.x.x.x) [target address](x.x.x.x)
```

ref: [windows - Ping IP with source IP? - Stack Overflow](https://stackoverflow.com/a/51000444)
