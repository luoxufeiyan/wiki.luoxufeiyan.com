# 数据卷

挂载一个主机目录作为数据卷
使用 -v 标记也可以指定挂载一个本地主机的目录到容器中去。
```
$ sudo docker run -d -P --name web -v /src/webapp:/opt/webapp training/webapp python app.py
```
上面的命令加载主机的 `/src/webapp` 目录到容器的 `/opt/webapp` 目录。这个功能在进行测试的时候十分方便，比如用户可以放置一些程序到本地目录中，来查看容器是否正常工作。本地目录的路径必须是绝对路径，如果目录不存在 Docker 会自动为你创建它。

* 查看目前的数据卷：
```
docker volume ls
```


* 新建数据卷：
```
docker volume create my-vol
```

* 查看指定数据卷：
```
docker volume inspect my-vol
```
