# Ubuntu 软件列表

记录一下我安装的Ubuntu程序，方便以后用。

## 网络浏览
  * Chrome浏览器
  * Tor Browser （tor browser launcher）或者`./start-tor-browser.desktop --register-app`
  * VPNgate: https://github.com/Dragon2fly/vpngate-with-proxy `alias vpngate='(cd /home/gao/Applications/vpngate-with-proxy && ./run cli)'`


[用做热点 hotspot](https://askubuntu.com/questions/318973/how-do-i-create-a-wifi-hotspot-sharing-wireless-internet-connection-single-adap)

## 办公类
  * Tusk 印象笔记客户端 [[https://github.com/klauscfhq/tusk/releases|下载]]

## 影音类
  * [OpenShot 视频编辑器](https://www.openshot.org/zh-hans/)

## 文件：
  * [Resilio](https://help.resilio.com/hc/en-us/articles/206178924-Installing-Sync-package-on-Linux)
  * [Duplicacy:A new generation cross-platform cloud backup tool](https://duplicacy.com/)


Resilio权限相关：

```
(base) gao@ThinkPad:~$ cat /etc/resilio-sync/config.json 
{
    "storage_path" : "/var/lib/resilio-sync/",
    "pid_file" : "/var/run/resilio-sync/sync.pid",

    "directory_root_policy" : "belowroot",
    "directory_root" : "/home/rslsync/",

    "webui" :
    {
        "listen" : "127.0.0.1:8889",
        "allow_empty_password" : false,
        "dir_whitelist" : [ "/home/rslsync/"]
    }
}

```

[How To Use BitTorrent Sync to Synchronize Directories in Ubuntu 12.04](https://www.digitalocean.com/community/tutorials/how-to-use-bittorrent-sync-to-synchronize-directories-in-ubuntu-12-04)

## 社交
  * Franz
  * telegram
  * Thunderbird

## 笔记本相关

指纹识别：

```
sudo apt install libpam-fprintd fprint-demo
```

电源管理：

```
sudo apt-get install tlp tlp-rdw tp-smapi-dkms acpi-call-dkms thermald powertop
```
