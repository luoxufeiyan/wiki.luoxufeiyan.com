# 磁盘用量
查看磁盘占用：
```
docker system df
```

清理虚悬镜像：
```
docker system prune
```
如需更加深度清理（只保留正在使用的容器以及数据卷，慎用！） 可以添加`-a`参数。