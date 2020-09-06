docker

### docker命令

```
选项
D
H
管理命令
checkpoint
container
image
network
node
plugin
secret
service
stack
swarm
system
volume
基本命令
attach
build
commit
cp
create
deploy
diff
events
exec
export
history
images
import
info
inspect
kill		杀死一个容器
load
login
logout
logs		查看容器日志
pause
port
ps			查看容器
pull		下载一个镜像
push		上传一个镜像
rename
restart
rm			删除指定容器
rmi
run
save
search		搜索一个镜像
start		启动一个容器
stats
stop		停止一个容器
tag
top
unpause
update
version		查看docker版本
wait
```



### 01-01docker安装

#docker.io基于centos版本docker
#docker-engine基于ubuntu版本docker
#docker-ce版本是docker.io的社区版本

```
yum -y install docker
systemctl start docker
systemctl enable docker
docker version 
docker info 显示docker信息，（确认服务运行）显示docker系统信息，镜像和容器数量
```

### 01-02docker配置加速

```
[root@localhost ~]# vim /etc/docker/daemon.json
{
  "registry-mirrors": ["https://qzbkb62r.mirror.aliyuncs.com"]
}
[root@localhost ~]# systemctl daemon-reload
[root@localhost ~]# systemctl restart docker

```

### 01-03docker开启网络转发

```

```

### 01-4docker镜像制作

#方法(1)使用docker commit 这个是保持container的当前状态到image后，然后生成对应image

```
docker commit 18a docker.io/centos:apache
```

#方法(2)使用docker build 使用dockerfile文件自动化制作image

```
参数解释
FROM		基于那个镜像
MAINTAINER	镜像创建者
RUN			安装软件包
ADD			
ADD
CMD			container启动时执行的命令,或者是服务 只能有一条
语法格式
docker build -t 父镜像名称:镜像tag Dockerfile文件所在路径
```

举例

```dockerfile
FROM docker.io/centos:latest
MAINTAINER mazhenjie@qq.com
RUN yum -y install httpd
ADD start.sh /usr/local/bin/start.sh
ADD index.html /var/www/html/index.html
CMD /usr/local/bin/start.sh
echo "/usr/sbin/httpd-DFOREGROUND" > start.sh
echo "docker image build test" > index.html
docker build -t docker.io/centos:httpd ./

```

### docker image 发布