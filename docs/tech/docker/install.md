# 安装 Docker

## Linux

```sh
curl -sSL https://get.docker.com/ | sh -s --mirror Aliyun
```
后面`--mirror Aliyun`为使用阿里云镜像，海外主机不需要添加。

设置Docker服务项开机自启
```
systemctl enable docker
```

ref:

- 换源：[Docker 镜像使用帮助 [LUG@USTC]](https://lug.ustc.edu.cn/wiki/mirrors/help/docker)


## Windows

### Windows Server

为老版本（Windows Server 2019）安装 docker CE。

```powershell
Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
.\install-docker-ce.ps1
```

ref: [Prepare Windows operating system containers | Microsoft Learn](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce#windows-server-1)