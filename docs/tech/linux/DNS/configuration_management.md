# DNS Configuration Management

## DNS 管理工具

在 Debian 系统中，常见的 DNS 管理工具和插件包括：

- **`systemd-resolved`**：一个 `systemd` 组件，负责管理 DNS 查询和解析。
- **`openresolv`**：一个管理 `/etc/resolv.conf` 文件的工具，负责为系统配置 DNS 服务器。`openresolv` 是 `resolvconf` 的现代化版本。

## DNS 配置文件

在 Debian 系统中，DNS 配置文件包括：

- **[/etc/resolv.conf](./resolv.md)**：存储 DNS 配置信息。由多个 DNS 管理工具动态生成。这个文件一般**不能**直接修改，会被其他工具覆盖。
- **/etc/systemd/resolved.conf**：`systemd-resolved` 配置文件，用于定义 DNS 和 DNS 后缀。


## DNS 管理工具如何工作

### `systemd-resolved` 管理 DNS

#### 作用：
`systemd-resolved` 是 `systemd` 系统的一部分，负责系统的 DNS 解析。它使用 **`/etc/systemd/resolved.conf`** 配置文件来管理 DNS 设置，并通过 **`/run/systemd/resolve/resolv.conf`** 或 **`/etc/resolv.conf`** 提供最终的 DNS 配置。

#### 配置文件：
- **`/etc/systemd/resolved.conf`**：该文件用于设置 DNS 服务器、DNS 后缀以及其它解析配置。
- **`/run/systemd/resolve/resolv.conf`**：由 `systemd-resolved` 动态生成的 DNS 配置文件。

#### 管理方式：
- 默认情况下，`systemd-resolved` 会将 **`/etc/resolv.conf`** 符号链接到 **`/run/systemd/resolve/resolv.conf`**。如果启用，`systemd-resolved` 将覆盖其他工具（如 `resolvconf` 或 `openresolv`）的配置。
- `systemd-resolved` 会维护一个 DNS 缓存，以提高查询效率。

#### 自定义 DNS 服务器：
- 编辑 **`/etc/systemd/resolved.conf`** 文件，在 **`[Resolve]`** 部分添加 DNS 服务器配置：
  ```ini
  [Resolve]
  DNS=8.8.8.8 8.8.4.4
  FallbackDNS=1.1.1.1 1.0.0.1
  ```
  - **`DNS`**：主 DNS 服务器。
  - **`FallbackDNS`**：备用 DNS 服务器。

- 配置完毕后，重新启动 `systemd-resolved` 服务：
  ```bash
  systemctl restart systemd-resolved
  ```

- 查看 DNS 状态：
  ```bash
  resolvectl status
  ```


### `openresolv` 管理 DNS

#### 作用：
`openresolv` 是 `resolvconf` 的现代化版本，用于管理 `/etc/resolv.conf` 文件。它通过收集来自多个来源（如 DHCP、VPN、静态配置等）的 DNS 设置，生成最终的 `/etc/resolv.conf` 文件。

#### 配置文件：
- **`/etc/resolv.conf`**：最终的 DNS 配置文件，由 `openresolv` 生成。
- **`/etc/resolvconf/resolv.conf.d/base`**：用户自定义的 DNS 配置，添加到 `/etc/resolv.conf` 中。
- **`/etc/resolvconf/resolv.conf.d/head`**：配置文件头部内容，一般包含注释信息。
- **`/etc/resolvconf/resolv.conf.d/tail`**：配置文件尾部内容，可以添加额外的 DNS 服务器或其他设置。

#### 管理方式：
- `openresolv` 会根据多个 DNS 配置来源（如 DHCP 或静态配置）生成 DNS 配置文件。
- 需要运行 `resolvconf -u` 命令来更新 `/etc/resolv.conf`。

#### 自定义 DNS 服务器：
1. 编辑 **`/etc/resolvconf/resolv.conf.d/base`** 文件：
   ```bash
   # 编辑 base 文件来设置自定义 DNS 服务器
   nameserver 8.8.8.8
   nameserver 8.8.4.4
   ```
2. 运行 `resolvconf -u` 更新 DNS 配置：
   ```bash
   resolvconf -u
   ```

### 常见问题排查：
1. **配置未生效**：
   - 检查是否有其他工具（如 `systemd-resolved` 或 `NetworkManager`）覆盖了 `/etc/resolv.conf`。
   - 使用 `resolvconf -u` 确保 `/etc/resolv.conf` 已更新。
   
2. **配置冲突**：
   如果系统同时启用了 `systemd-resolved` 和 `openresolv`，可能会出现冲突。建议禁用 `systemd-resolved` 或在 `/etc/resolv.conf` 中配置优先级。

3. **云厂商的设置**：
    云服务商（如 AWS、GCP、Azure）可能会使用自定义的 DNS 设置。在云环境中，`cloud-init` 用于自动配置网络参数，包括 DNS 设置。`cloud-init` 会根据云平台提供的数据源（如 AWS、Azure）配置 DNS 服务器。

    `/etc/cloud/cloud.cfg.d/50-cloud-init`**：由 `cloud-init` 管理的网络配置文件，可能会设置 DNS 服务器，有些管理工具会使用网络配置文件中的值。