

### 官方一键安装脚本

```bash
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && chmod 755 msfinstall && ./msfinstall
```



### Postgresql数据库

```bash
yum -y install https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
yum install -y postgresql10-server postgresql10-contrib
```

### 初始化

```bash'
/usr/pgsql-10/bin/postgresql-10-setup initdb
```

### 设置开机自启,然后启动数据库

```bash
systemctl enable postgresql-10   
systemctl start postgresql-10 
```

### msf连接postgresql

#### 首先初始化数据库：

```bash
cd /opt/metasploit-framework/bin/
#不能以root用户初始化数据库
useradd msf
su msf
#初始化数据库
bash msfdb init
#提示
[?] Initial MSF web service account username? [msf]: msf
[?] Initial MSF web service account password? (Leave blank for random password):  #直接回车
#创建完成后在msf用户目录会生成一个.msf目录里面会有一个database.yml文件
```

#### 切换回root用户执行

```
#该操作将原配置文件覆盖
cp /home/msf/.msf4/database.yml /opt/metasploit-framework/embedded/framework/config/
```

#### 我们再启动msf，数据库连接正常

![image-20200828013119028](https://blo-g.oss-cn-beijing.aliyuncs.com/mkdir/image-20200828013119028.png)