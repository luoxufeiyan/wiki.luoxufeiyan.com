# resolv.conf

`resolv.conf` 是一个配置文件，它包含了 DNS（域名系统）解析器的配置。它被许多网络工具和程序用来确定如何进行 DNS 查询。

## 位置

`/etc/resolv.conf`

## 文件内容

这个文件的内容指定了 DNS 解析器的行为，通常包括 DNS 服务器地址、域名搜索顺序等设置。一个基本的 `resolv.conf` 文件可能如下所示：

```bash
# /etc/resolv.conf

nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com
```

### 主要字段说明

- `nameserver <IP address>`：指定 DNS 服务器的 IP 地址。通常你可以指定多个 DNS 服务器，系统会按照顺序尝试这些服务器。
- `search <domain>`：指定一个域名后缀，DNS 查询时会自动添加这个后缀。这对于简化局域网内的主机名解析很有帮助。
- `domain <domain>`：指定默认域名后缀，通常与 `search` 类似，但不支持多个域名。

## 如何修改

不推荐直接编辑 `resolv.conf` 文件来修改 DNS 配置。在某些系统上，`resolv.conf` 文件是由其他工具（如 `systemd-resolved` 或 `openresolv`）自动管理的。在这种情况下，手动编辑 `resolv.conf` 可能会被系统覆盖。

