# Ubuntu常用PPA

### Telegram
```
sudo add-apt-repository ppa:atareao/telegram
sudo apt-get update
sudo apt-get install telegram
```

### Openshot
```
sudo add-apt-repository ppa:openshot.developers/ppa
sudo apt-get update
sudo apt-get install openshot-qt 
```

### Nodejs
```
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get update
sudo apt install nodejs
```

### Yarn
```
 curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
 echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
 sudo apt-get update && sudo apt-get install yarn

```

### Resilio
```
echo "deb http://linux-packages.resilio.com/resilio-sync/deb resilio-sync non-free" | sudo tee /etc/apt/sources.list.d/resilio-sync.list
curl -LO http://linux-packages.resilio.com/resilio-sync/key.asc && sudo apt-key add ./key.asc
sudo apt-get update
sudo apt-get install resilio-sync
```

### Ulauncher
```
sudo add-apt-repository ppa:agornostal/ulauncher
sudo apt-get update
sudo apt-get install ulauncher
```

### Spotify
```
curl -sS https://download.spotify.com/debian/pubkey.gpg | sudo apt-key add - 
echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
sudo apt-get update && sudo apt-get install spotify-client
```

### f.lux
注意Ubuntu 16.04 后不可用，建议使用 `redshift`
```
sudo add-apt-repository ppa:nathan-renniewaldock/flux
sudo apt-get update
sudo apt-get install fluxgui
```

### TLP
适用于笔记本的电源管理工具。
[[http://linrunner.de/en/tlp/tlp.html|linrunner.de: TLP —— Linux Advanced Power Management]]
```
sudo add-apt-repository ppa:linrunner/tlp
sudo apt-get update
sudo apt-get install tlp
```

安装完成后需手动启动`sudo tlp start`，随后tlp会随设备开机运行。

### UNetbootin
制作USB启动盘的工具。
```
sudo add-apt-repository ppa:gezakovacs/ppa
sudo apt-get update
sudo apt-get install unetbootin
```

### Tor
【非官方】`torbrowser-launcher`，已加入Ubuntu软件中心。下载后仍需要下载tor-browser。

```
sudo add-apt-repository ppa:micahflee/ppa
sudo apt-get update
sudo apt-get install torbrowser-launcher
```

【非官方】`tor-browser`，非官方维护。
```
sudo add-apt-repository ppa:webupd8team/tor-browser
 sudo apt-get update
 sudo apt-get install tor-browser
```

### papirus

```
sudo add-apt-repository ppa:papirus/papirus
sudo apt-get update
sudo apt-get install papirus-icon-theme
```

### Typora
```
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -
sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt-get update
sudo apt-get install typora
```

### 扩展阅读
[21 Must-Have Apps for Ubuntu (2020 Edition) - OMG! Ubuntu!](https://www.omgubuntu.co.uk/2016/12/21-must-have-apps-ubuntu)