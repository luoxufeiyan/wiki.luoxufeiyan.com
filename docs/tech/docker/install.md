# 安装 Docker

```
curl -sSL https://get.docker.com/ | sh -s --mirror Aliyun
```
后面`--mirror Aliyun`为使用阿里云镜像，海外主机不需要添加。

换源：[[https://lug.ustc.edu.cn/wiki/mirrors/help/docker|Docker 镜像使用帮助 [LUG@USTC]]]

设置Docker服务项开机自启
```
systemctl enable docker
```