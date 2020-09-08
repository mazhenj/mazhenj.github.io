# docker

## docker基本操作

#### 01docker命令

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



#### 01-01docker安装

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

#### 01-02docker配置加速

```
[root@localhost ~]# vim /etc/docker/daemon.json
{
  "registry-mirrors": ["https://qzbkb62r.mirror.aliyuncs.com"]
}
[root@localhost ~]# systemctl daemon-reload
[root@localhost ~]# systemctl restart docker

```

#### 01-03docker开启网络转发

```

```

### docker镜像制作

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

#### 02-01save image to tarball

```
#语法格式
docker save -o 导出的镜像名字.tar 本地镜像名字:镜像标签
docker save -o centos.tar docker.io/centos:latest
#导入镜像
docker load -i centos.tar 
```

![image-20200907001001100](https://blo-g.oss-cn-beijing.aliyuncs.com/mkdir/image-20200907001001100.png)

#### 02-02push image to Docker Hub

![image-20200907002936964](https://blo-g.oss-cn-beijing.aliyuncs.com/mkdir/image-20200907002936964.png)

```
docker login 登录
docker push mazhenjie/hex
docker pull mazhenjie/hex:apache
```

#### 02-03使用阿里云私有仓库

阿里云注册 省略

```
docker login --username=1853244596@qq.com registry.cn-hangzhou.aliyuncs.com
docker tag 0d120b6ccaa8 registry.cn-hangzhou.aliyuncs.com/enablee/hex:1.0
docker push registry.cn-hangzhou.aliyuncs.com/enablee/hex:1.0
具体参考阿里云官方手册即可
```

### container端口映射

```
 docker run  -itd -p 80:80 587 bash 
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --reload
firewall-cmd --list-all
```

### container进入容器的四种方式

#### 03-01 exec

```
docker exec -it id bash
```

### container配置ssh远程登陆

配置稍微复杂 日后再说

## docker 容器命名 和资源配置



#### 01-01容器命名语法

```
docker run -d --name 容器实例名 容器镜像名字 要执行的命令
docker run -d --name apache docker.io/centos:httpd bash
```

#### 01-02容器重命名语法

```
docker rename 旧容器名字 新容器名字
docker rename apache apache222
```

#### 01-03创建docker实例时指定主机名

```
语法
docker run -it --name 容器名 -h 指定主机名 镜像 bash
docker run  -it --name  httpd -h node1 docker.io/centos:httpd bash		
```



#### 01-04docker设置开启自启动

```
#语法
docker run --restart=always -itd --name test centos bash
#实例
docker run --restart=always -itd --name hox docker.io/centos:httpd bash
```

docker容器重启策略
no 默认策略 
on-failure 在容器非正常退出(状态为0)时才重启容器 
on-failure:3 在容器非正常退出时,最多重启三次
always 在容器退出时总是重启容器
unless-stopped 在容器退出时,总是重启容器,不考虑docker守护进程启动时就已经停止的容器

扩展

如果创建时没有指定, 通过update命令设置

```
#语法
docker update --restart=always id
```

 docker容器资源配额控制之CPU

```bash
[root@localhost dockerbuild]# docker run --help | grep cpu
      --cpu-count int                  CPU count (Windows only)
      --cpu-percent int                CPU percent (Windows only)
      --cpu-period int                 Limit CPU CFS (Completely Fair Scheduler) period 周期 指定容器对CPU的使用,要在多长时间内,做一次重新分配
      --cpu-quota int                  Limit CPU CFS (Completely Fair Scheduler) quota  用来指定在这个周期内,最多可以有多少时间片来跑这个容器
      --cpu-rt-period int              Limit CPU real-time period in microseconds
      --cpu-rt-runtime int             Limit CPU real-time runtime in microseconds
  -c, --cpu-shares int                 CPU shares (relative weight)CPU共享 相对权重
      --cpus decimal                   Number of CPUs (default 0.000)
      --cpuset-cpus string             CPUs in which to allow execution (0-3, 0,1)
      --cpuset-mems string             MEMs in which to allow execution (0-3, 0,1)
```

#### 01-01 容器资源配额控制

```
--cpu-shares
docker run -it --cpu-shares 512 centos /bin/bash
cat /sys/fs/cgroup/cpu/cpu.shares
```

![image-20200907163523666](https://blo-g.oss-cn-beijing.aliyuncs.com/mkdir/image-20200907163523666.png)

#### 01-02CPU周期控制

```
--cpu--period
--cpu--quota
单位微秒 cpu--period 最小值1000微秒 最大值1秒(10^6) 默认值0.1秒(100000微秒) cpu-quota默认值-1 表示不作控制
时间单位换算 1秒=1000毫秒 1毫秒=1000微秒
实例:设置docker实例每一秒只能使用单个cpu的0.2秒时间 = cpu--quota 1000000(1秒) cpu--period 2000000 (0.2秒)
```

```
docker run -it --cpu-period 1000000 --cpu-quota 2000000 docker.io/centos:httpd bash
cat /sys/fs/cgroup/cpu/cpu.cfs_period_us
cat /sys/fs/cgroup/cpu/cpu.cfs_quota_us
```

![image-20200907192702762](https://blo-g.oss-cn-beijing.aliyuncs.com/mkdir/image-20200907192702762.png)



#### 01-03 CPU core核心控制

```bash
--cpuset-cpus
--cpuset--mems
```

```
待补充
```

















## docker 配置IP和私有仓库