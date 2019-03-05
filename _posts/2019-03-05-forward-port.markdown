---
layout:     post
title:      "ss端口转发"
subtitle:   " \"端口转发\""
date:       2019-03-05 
author:     "heliang"
header-img: "img/contact-bg.jpg"
catalog: true
tags:
    - ss
---


### 一、背景

- ss
- mtproto

公司wifi直连美国vps，ip经常被ban，而4G和其他的Wi-Fi却没有这个问题。为了解决这个问题，参考其他的方法，决定搭建中间路由服务器转发到vps。自己--->转发服务器--->vps(ss, mtproto)
涉及到端口转发的问题，特此记录一下。

### 二、关于haproxy
centos7下安装
```
yum -y install haproxy
```

编辑配置文件不同端口转发
```
 vi /etc/haproxy/haproxy.cfg
```

```
global
    ulimit-n  51200

defaults
    log    global
    mode    tcp
    option    dontlognull
        timeout connect 5000
        timeout client  50000
        timeout server  50000

frontend ss-in
    bind *:relay_server_port
    default_backend ss-out

backend ss-out
    server server1 proxy_server_ip:proxy_server_port maxconn 20480
```

如果是中继多端口都要被转发， bind改为
```
bind *:1000-2000
```
表示1000-2000的端口都会被转发到目标服务器

设置开机启动：```systemctl enable haproxy```

启动服务：```systemctl start haproxy```

***使用时候只需要将目标服务器的ip和端口改为中转服务器的即可***。


### 三、telgram专用协议mtproto

下载和安装

```
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/mtproxy.sh && chmod +x mtproxy.sh && bash mtproxy.sh
```

### 四、firewall 实现端口转发
- 开启防火墙伪装
```
firewall-cmd --add-masquerade --permanent    //开启后才能转发端口
```

- 开始ip转发功能

```
vi /etc/sysctl.conf
```

```
net.ipv4.ip_forward = 1
```
保存文件后，输入命令sysctl -p生效
- 添加转发规则

```
firewall-cmd --add-forward-port=port=80:proto=tcp:toport=8080:toaddr=233.233.233.233 --permanent
```
此规则的意思是将本机80端口转发到233.233.233.233的8080端口
如果toaddr缺省的话，就是本机的80到本机的8080端口转发。

- 查看现有的转发规则

```
firewall-cmd --list-forward-ports
```

-  firewall-cmd --reload 










