# ngrok 配置文件

适用于ngrok 1.7 版本。

## ngrok.cfg
```
server_addr: "global.luoxufeiyan.com:4443"
trust_host_root_certs: false

tunnels:
  http:
    subdomain: "www"
    proto:
      http: "8081"
      
  https:
    subdomain: "www"
    proto:
      https: "8082"
      
  web:
    proto:
      http: "8050"
  tcp:
    proto:
      tcp: "8001"
    remote_port: 5555
 
  ssh:
    remote_port: 2222
    proto:
      tcp: "22"
```

## Docker

[[https://hub.docker.com/r/sequenceiq/ngrokd/|https://hub.docker.com/r/sequenceiq/ngrokd/]]

[[https://segmentfault.com/a/1190000010338848|centos下自己架设ngrok服务器（内网测试神器） - 个人文章 - SegmentFault]]

## OpenWRT


init.d script

自建ngrok服务端需在script中去掉token判断。


```
#!/bin/sh /etc/rc.common

START=99

local shost
local sport
local token

ngrok_add_rule() {
	local localip
	local lport
	local rport
	local proto
	local sdname
	local domaintype
	local cfg="$1"
	local rules="$2"

	config_get localip $cfg ip
	config_get lport $cfg lport
	config_get rport $cfg rport
	config_get proto $cfg protocol
	config_get sdname $cfg subdomain
	config_get domaintype $cfg domaintype

	if [ -z "$localip" ]; then
		return 0
	fi

	proto=$(echo $proto| tr '[A-Z]' '[a-z]') 

	
	if [ "$proto" == "tcp" ]; then
	 append $rules "/usr/bin/ngrokc -SER[Shost:$shost,Sport:$sport,Atoken:$token] -AddTun[Type:tcp,Lhost:$localip,Lport:$lport,Rport:$rport] &  $N"	
	else
	 if [ "$domaintype" == "1" ]; then
	  append $rules "/usr/bin/ngrokc -SER[Shost:$shost,Sport:$sport,Atoken:$token] -AddTun[Type:$proto,Lhost:$localip,Lport:$lport,Hostname:$sdname] &  $N"
	 else
	  append $rules "/usr/bin/ngrokc -SER[Shost:$shost,Sport:$sport,Atoken:$token] -AddTun[Type:$proto,Lhost:$localip,Lport:$lport,Sdname:$sdname] &  $N"
	 fi
	fi

}


start() {
	config_load ngrok
	config_get_bool ngrok_enable config enable 0
	config_get shost config server ""
	config_get sport config port ""
	config_get  token config token ""
	if [ $ngrok_enable == 0 ]; then
		#stop
		return 0
	fi
	if [ -z "$shost" -o -z "$sport" -o -z "$token" ]; then
		return 0
	fi
	local ngrok_rules
	config_foreach ngrok_add_rule rules ngrok_rules
	echo -e "$ngrok_rules" |sh

}

stop() {
	killall -9 ngrokc
}

restart() {
	stop
	start
}


```

ngrok config

```
config ngrok 'config'
	option port '4443'
	option server 'ngrokserver.luoxufeiyan.com'
	option enable '1'
	option token ''

config rules
	option protocol 'HTTP'
	option ip '192.168.2.1'
	option lport '80'
	option subdomain 'router'
	option domaintype '0'

config rules
	option protocol 'TCP'
	option rport '13304'
	option ip '192.168.2.1'
	option lport '22'
	option domaintype '0'


```