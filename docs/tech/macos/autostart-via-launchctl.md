# 使用 launchd 使脚本开机自动启动

以ShadowSocks为例。

在`~/Library/LaunchAgents/`目录下新建`com.fledding.shadowsocks.plist`文件：


```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.fledding.shadowsocks</string><!--需要与文件名保持一致-->
    <key>ProgramArguments</key>
    <array>
        <string>/usr/local/bin/sslocal</string>
        <string>-c</string>
        <string>/Users/gao/.config/shadowsocks.json</string>
    </array>
    <key>KeepAlive</key><!--后台保持运行-->
    <true/>
    <key>RunAtLoad</key><!--加载时候运行-->
    <true/>
    <key>UserName</key>
    <string>charles</string>
    <key>GroupName</key>
    <string>staff</string>
</dict>
</plist>
```

然后执行`launchctl load com.fledding.shadowsocks.plist`文件即可，即刻生效，且重启后会自动启动。

[[https://sexywp.com/use-launchd-to-start-shadowsocks.htm|[Mac]使用launchd配置开机自动启动shadowsocks – Becomin' Charles]]
