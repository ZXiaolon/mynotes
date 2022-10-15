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
*  Docker Registry：
Docker使用C/S架构模式，使用远程api来管理和创建Docker容器。
Docker容器根据Docker镜像来进行创建。
