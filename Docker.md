# This is Docker notes

Docker是开源的应用容器引擎，基于GO语言。特点：轻量级、可移植。Docker分为CE和EE。

**Docker的应用场景**
* Web应用的自动化打包和发布；
* 自动化测试和持续集成、发布；
* 在服务型环境中部署和调整数据库或其他后台应用；等等


**Docker的基本概念**
* 镜像(Image)：Docker镜像，相当于一个root文件系统。类似于模板的作用。
* 容器(Container)：镜像-容器的关系类似于面向对象层序设计中的类和实例的关系。镜像是静态的定义，容器时镜像运行时的实体。容器可以被创建、启动、停止和删除等。
* 仓库(Repository): 代码控制中信，用来保存镜像。
  * Docker Registry：包含仓库(repository)的仓库。Repository保存这软件的各个版本。通过`<仓库名>:<标签>`来指明软件的具体版本的镜像，如不给出采用latest作为默认标签。
Docker使用C/S架构模式，使用远程api来管理和创建Docker容器。
Docker容器根据Docker镜像来进行创建。

## Docker安装、卸载、启动、验证
1. 安装
```bash
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```
或者
```bash
curl -sSL https://get.daocloud.io/docker | sh
```
2. 卸载
```bash
sudo yum remove docker docker-client docker-client-latest docker-latest-logrotate docker-logrotate docker-engine
```
3. 设置Docker仓库
```bach
sudo yum-config-manager --add-repo http://xxxx
```
4. 启动Docker
```bach
sudo systemctl start docker
```
5. 验证
```bash
sudo docker run hello-world
```
6.卸载docker
```bash
yum remove docker-ce
```
```bash
rm -rf /var/lib/docker
```

7. 镜像加速
在/etc/docker/daemon.json文件添加如下内容
`{"registry-mirrors":["https://reg-mirror.qiniu.com/]}`
之后进行服务重启
```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

## Docker入门
### Docker基本启动方式
Docker允许在**容器**内运行应用程序，使用docker run命令来运行应用程序。
1. 启动docker
 ```bash 
 docker run ubuntu:15.10 /bin/echo "hello world"
 // 或者进入应用
 docker run -i -t ubuntu:15.10 /bin/bash
 //后台启动
 docker run -d ubuntu:15.10 /bin/sh 
 ```
 
2. 查看运行的容器
```bash
docker ps
```
3. 停止运行的容器
```bash
docker stop docker_id or docker_name
```

启动镜像
```bash
docker start containerId
```

进入容器
`docker attach`或者`docker exec`推荐使用后者，这样从容器退出不会导致容器停止。

导入/导出容器
导出本地某个容器:将container导出到container.tar
```bash
docker export <containerId> >container.tar
```
导入容器：将快照文件ubuntu.tar导入到镜像文件/test/ubuntu:v1
```bash
cat docker/ubuntu.tar | docker import container.tar -test/ubuntu:v1

docker import http://xxxx
```

删除容器
```bash
docker rm -f containerId
```

启动webapp并映射对外窗口(将对外窗口映射到程序内5000端口)
```bash
docker pull training/webapp
docker run -d -p 80:5000 training/webapp python app.py
```

















### Docker帮助
`Docker`命令会显示关于Docker的基本使用命令。
`Docker command --help`command替换成要查询使用的命令例如run查看帮助。

**获取镜像**
`docker pull ubutun`拉取ubuntu的镜像。


### Docker镜像操作
* 显示本地镜像列表`docker images`
* 获取镜像：`docker pull imageName`
* 查找镜像：`docker search imageName`
* 删除镜像：`docker rmi image`

* 更改镜像有以下两种方式：
  1. 从已有的**容器**中更新镜像，并提交镜像
    * 在对容器操作之后
    ```bash
    docker commit -m="about commit info" -a="author" containerId author/ubuntu:v2
    ```
  2. 使用Dockerfile指令来创建镜像
    * 采用docker build命令从零创建新的镜像。在次之前我们需要创建Dockerfile文件。
    ```
    docker build -t imageName .
    ```
    imageName:要创建的目标镜像名
    .：Dockerfile文件所在目录，可以为绝对路径
    
**Dockerfile文件介绍**
Dockerfile是一个用来构建镜像的文本文件，文本内容包含了构建镜像所需要的指令和说明。
使用Dockerfile构建一个镜像流程：以定制nginx镜像为例。
1.在空目录创建一个Dockerfile文件，文件内容如下：
```
FROM nginx
RUN echo 'xxxx' > /user/share/nginx/html/index.html
```
`FROM`：获取基础镜像这是里nginx；
`RUN`：用于执行命令
```
shell格式：
RUN <命令行命令>
exec格式：
RUN ["可执行文件","参数1","参数2",..]
```
注意：Dockerfile的指令每执行一次会在docker上新建一层，容易造成镜像膨胀。

指令介绍
```
CMD:类似RUN指令，用于运行程序。如Dockerfile存在多个CMD文件，仅运行最后一个。
CMD:在docker run时运行
RUN：在docker build时运行

```


2.开始构建镜像
下面用Dockerfile构建nginx:v3。其中.为上下文路径
```
$ docker build -t nginx:v3 .
```

### Docker容器连接
**网络端口映射**
```bash
docker run -d -P/-p
```
-P：容器内端口随机**映射**到主机的端口
-p：容器内端口**绑定**到指定的主机端口


**Docker容器互联**
通过网桥连接两个容器
1.新建一个网络
2.查看网络
3.创建并运行一个容器1，加入网络
4.创建并运行一个容器2，加入网络
5.两个容器进行通信。ping

```bash
$ docker run -d P --name runoob training/webapp python app.py
$ docker network ceate -d bridge test-net
$ docker network ls
$ docker run -itd --name test1 --network test-net ubuntu /bin/bash
$ docker run -itd --name test2 --network test-net ubuntu /bin/bash
```
**DNS的配置**
全部批量设置:修改/etc/docker/daemon.json文件
```json
{
"dns":[
"114.114.114.114",
"8.8.8.8"
]
}
```
单独对某个容器进行修改
```bash
docker run -it -rm -h host_ubuntu --dns=114.114.114.114 --dns-search=test.com ubuntu
```



































