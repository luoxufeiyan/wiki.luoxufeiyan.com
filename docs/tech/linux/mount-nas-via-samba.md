# 通过 samba 挂载 NAS 文件夹

尽管 NAS 支持 WebDav，但是 davfs 会产生大量的缓存文件，给我的印象很不好。所以还是用 samba 协议挂载。

安装 samba 客户端

```
sudo apt install samba-client cifs-utils
```

如果要挂载的分区格式是 nfs 的话还需要装：

```
sudo apt-get install nfs-common
```

随后 ~~使用这段被祝福的代码~~ 挂载就可以了：

```
sudo mkdir /mnt/nas0
sudo mount -t cifs //192.168.0.3/Public /mnt/nas0 -o user=luoxufeiyan,password=MyPasswd
```

单次挂载也可以直接使用`mount.cifs`命令，方便测试和临时使用：

```shell
mount.cifs [//192.168.0.10/PATHDIR](//192.168.0.10/PATHDIR) /mnt/MOUNT_POINT -o user=USER,iocharset=utf8
```

匿名挂载： `mount -t cifs //192.168.0.5/Public /mnt/share -o user=,file_mode=0777,dir_mode=0777,unc=\\\\192.168.0.5\\Public`

如果需要非 root 也可写的话：

```
sudo mount -t cifs //192.168.0.3/Public /mnt/nas0 -o user=luoxufeiyan,password=MyPasswd,rw,uid=0,gid=0,dir_mode=0777,file_mode=0777
```

如果要永久挂载的话需要写`/etc/fstab`文件,详：[MountWindowsSharesPermanently - Ubuntu Wiki](https://wiki.ubuntu.com/MountWindowsSharesPermanently)。

```
//192.168.0.3/Public  /mnt/spc  cifs  user=luoxufeiyan,password=MyPasswd,workgroup=WORKGROUP,file_mode=0777,dir_mode=0777,uid=pi,gid=pi,forceuid,forcegid  0  0

```

匿名挂载： `//192.168.0.5/Public /mnt/share cifs username=,file_mode=0777,dir_mode=0777 0 0`

aria2 或者 transmission 可能会遇到 allocation 问题，需在 transmission 的配置中关闭 preallocation。

对于树莓派，选择启用 `Wait for Network at Boot`。

1. 输入`sudo raspi-config`
2. `Boot Options > Wait for Network at Boot > Yes `

## Ref

- [[OpenWrt Wiki] CIFS Client](https://openwrt.org/docs/guide-user/services/nas/cifs.client)
