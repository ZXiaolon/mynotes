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
























