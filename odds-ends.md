

## Proxy Server
> :star: [refer](https://thief.one/2017/02/22/Shadowsocks%E6%8A%98%E8%85%BE%E8%AE%B0/)

* pip
```
yum -y install epel-release
yum -y install python-pip
```
* shadow
```
pip install shadowsocks
```
* vim /etc/shadowsocks/config.json
```
{
"server":"",     
"server_port":8000,  
"local_address":"127.0.0.1",
"local_port":1080, 
"password":"xxx",   
"timeout":300,
"method":"aes-256-cfb",
"fast_open":false
}
```

* start
```
ssserver -c /etc/shadowsocks/config.json -d start 
```

* 设置开机启动
> 将启动的命令加入到/etc/rc.local文件的最后
```
vi /etc/rc.local
```


## Client
1. [Releases · shadowsocks/shadowsocks-qt5](https://github.com/shadowsocks/shadowsocks-qt5/releases)
2. [shadowsocks-windows](https://github.com/shadowsocks/shadowsocks-windows/releases)
3. [all client](https://shadowsocks.org/en/download/clients.html)

## Refer
1. [Shadowxsocks](https://teddysun.com/486.html)
2. [Shadowsocks | ](http://www.vuln.cn/8555)


:tada:[shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev)
* docker
```
docker pull shadowsocks/shadowsocks-libev
docker run -e PASSWORD=<password> -p<server-port>:8388 -p<server-port>:8388/udp -d shadowsocks/shadowsocks-libev
```

## FAQ

It's quite tricky here. To make UDP and kcptun both work, you have to add additional parameters to plugin_opts. For example:

* On the server
```
ss-server -c config.json --plugin kcp-server -s 443 --plugin-opts "listen=0.0.0.0:444" -u
```

* On the client
```
ss-local -c config.json --plugin kcp-local --plugin-opts "remoteaddr=server_ip:444" -u
```
