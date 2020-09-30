layout:     post
title:      web常见漏洞
subtitle:   
date:       2020-8-1
author:     xiwang
header-img: img/tag-bg-o.jpg
catalog: true
tags:

    - xss



# XSS

### XSS原理

xss全称(跨站脚本攻击),主要是由于web应用程序对用户的输入过滤不足而产生的,恶意攻击者往往往web页面里面插入恶意脚本代码,当用户游览该页时,嵌入其中的脚本代码会被执行,攻击者可以利用此攻击对受害者用户,采取cookie资料窃取,会话劫持,调取欺骗等各种攻击

### XSS分类

反射型

存储型

DOM型

### 其他类别XSS

mXSS (突变型XSS)

UXSS(通用型XSS)

Flash XSS

UTF-7 XSS

MHTML XSS

CSS XSS

VBScript XSS

### XSS危害

- 网络钓鱼 包括获取各类用户账号
- 窃取用户cookie资料 从而获取用户隐私信息,或者利用用户身份信息,进一步对网站执行操作
- 劫持用户(游览器)会话,从而执行任意操作,例如非法转账,强制发表日志,电子邮件等
- 恶意弹出广告页面,刷流量
- 网页挂马
- 进行恶意操作,例如串改页面信息,删除文章
- 进行大量客户端攻击,例如ddos等
- 获取客户端信息,如用户的游览历史,真实IP,开放端口等
- 控制受害者机器,像其他网站发起攻击
- 结合其他漏洞例如csrf,实施进一步危害
- 提升用户权限,包括进一步,网站渗透
- 传播跨站脚本,蠕虫等

### 反射型XSS

 又叫做非持久性XSS,这种攻击方式往往具有一次性, 只在用户单击时触发]

```html
<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="Generator" content="EditPlus®">
  <meta name="Author" content="">
  <meta name="Keywords" content="">
  <meta name="Description" content="">
  <title>XSS-LEVEL1反射XSS</title>
 </head>
 <body>
  <H1>反射XSS-LEVEL1 By xiwang</H1>
  <HR>
  <BR/>
  <H4>输入您需要提交的内容</H4>
<form action="" method="get">  
    <input type="text" name="xss"/>  
    <input type="submit" value="提交"/>  
</form>  
<?php  
    $xss = @$_GET['xss'];  
    if($xss!==null){
        echo "<br/>";
        echo "您提交的内容是:".$xss;  
    }
?>

 </body>
</html>
```

  上述代码中,首先包含一个表单,用于向页面自己发送GET请求,带一个名为XSS的参数,然后PHP会读取该参数,如果不为空,则直接打印出来,这里不存在,任何过滤

### 练习XSS平台

https://xss-quiz.int21h.jp/