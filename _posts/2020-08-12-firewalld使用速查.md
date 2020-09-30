layout:     post
title:      firewall
subtitle:   
date:       2020-8-1
author:     xiwang
header-img: img/tag-bg-o.jpg
catalog: true
tags:
    - Linux

常用命令

```
#安装
yum -y install firewalld
#启动
systemctl start firewalld
#查看状态
systemctl status firewalld firewall-cmd -state
#禁止开机自动启动
systemctl disable firewalld
#停止
systemctl stop firewalld
```

配置

```
firewall-cmd --version
firewall-cmd --help
firewall-cmd --state
#查看区域信息
firewall-cmd --get-active-zones
#查看指定借口所属区域
firewall-cmd --get-zone-of-interface=ens33
#拒绝所有包
firewall-cmd --panic-on
#取消拒绝所有包
firewall-cmd --panic-off
#查看是否拒绝
firewall-cmd --query-panic
#更新防火墙规则
firewall-cmd --reload
firewall-cmd --complete-reload
#列出所有支持的zone
firewall-cmd --get-zones
#查看当前默认zone
firewall-cmd --get-default-zone
#设置默认接口区域
firewall-cmd --set-default-zone=public
#将接口添加到区域 默认接口都在public
firewall-cmd --zone=public --add-interface=ens33
备注 永久生效加上 --permanent 然后 reload 防火墙
#打开端口
irewall-cmd --zone=dmz --list-ports
#加入一个端口到区域
firewall-cmd --zone=dmz --add-port=8899/tcp
#打开一个服务 类似将端口可视化
firewall-cmd --zone=work --add-service=smtp
#移除一个服务
firewall-cmd --zone=work --remove-service=smtp
#列出默认区域的信息
firewall-cmd --list-all
#列出其他区域的信息
firewall-cmd --zone=work --list-all
#查询活动的区域
firewall-cmd --get-active-zones
#
```

