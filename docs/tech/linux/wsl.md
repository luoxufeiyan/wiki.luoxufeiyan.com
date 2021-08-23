# WSL

又爱又恨的 Windows Subsystem Linux。

## 文件类

### 权限相关

解决不能修改`/mnt/c`下权限的问题：

需要重新挂载C盘并添加`metadata`标签。

```
sudo umount /mnt/c
sudo mount -t drvfs C: /mnt/c -o metadata
```

[Chmod/Chown WSL Improvements](https://devblogs.microsoft.com/commandline/chmod-chown-wsl-improvements/)