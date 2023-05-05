# Nuget

### 为 Nuget 设置代理

在 C:\Users\UserName\AppData\Roaming 下找到 NuGet\NuGet.Config 文件，添加下面这一段：

```xml
  <config>
    <add key="http_proxy" value="http://127.0.0.1:1080" />
  </config>
```

ref: [NuGet behind a proxy - Stack Overflow](https://stackoverflow.com/a/15463892/3886059)