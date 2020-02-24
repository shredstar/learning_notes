# Docker - 从入门到实践

## C01 Docker简介
* 关键技术 - 操作系统层面的虚拟化技术
	* cgroup, namespace
	* Union FS
* 引擎演进：LXC -> libcontainer -> runC和containerd
* 容器没有自己的内核，也没有进行硬件虚拟。
* Docker的关键优势
	* 一致的运行环境
	* 持续交付和部署
	* 更轻松的维护和扩展：基于现有镜像做扩展

## 基本概念
* 镜像
	* Doker镜像，就相当于一个root文件系统（让系统跑起来的最小文件集）
	* Docker 镜像是一个特殊的文件系统，除了提供容器运行时所需的程序、库、资源、配置等文 件外，还包含了一些为运行时准备的一些配置参数（如匿名卷、环境变量、用户等）。镜像 不包含任何动态数据，其内容在构建之后也不会被改变。
	* 分层存储：Docker利用Union FS技术，采用**多层**文件系统组成镜像文件
		* 在构建镜像的时候，需要额外小心，每一层尽量只包含该层需要添加的东西，任何额外的东西应该在该层构建结束前清理掉。
		* 分层存储的特征还使得镜像的复用、定制变的更为容易。甚至可以用之前构建好的镜像作为 基础层，然后进一步添加新的层，以定制自己所需的内容，构建新的镜像。

* 容器
	* 镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
	* 容器的实质是进程，但与直接在宿主执行的进程不同，容器进程运行于属于自己的独立的命名空间。 
	* 每一个容器运行时，是以镜像为基础层，在其上创建一个当前容器的存储层，我们可以称这个为容器运行时读写而准备的存储层为容器存储层。 
		* 容器存储层的生存周期和容器一样，容器消亡时，容器存储层也随之消亡。
		* 按照 Docker最佳实践的要求，容器不应该向其存储层内写入任何数据，容器存储层要保持无状态化。
		* 所有的文件写入操作，都应该使用数据卷（Volume）、或者绑定宿主目录，在这些位置的读写会跳过容器存储层，直接对宿主（或网络存储）发生读写，其性能和稳定性更高。

* 仓库
	* Docker Registry：一个集中的存储、分发镜像的服务。
	* Docker Registry包含多个仓库（Repository)，一个仓库包含多个标签（Tag），一个标签对应一个镜像。一个镜像可以对应多个标签。
	* 仓库即软件，标签即版本。默认标签为最新版本。例如：ubuntu:14.04，ubuntu = ubuntu.latest。
	* 仓库名 = Docker Registry下用户名/软件名，例如，shredstar/nginx-proxy
	* Docker Registry公开服务
		* Docker Hub
		* Quay.io
		* Google Container Registry（Kubernetes）

## C02 安装Docker
* CE：社区版，免费。
	* Stable版，每个季度发行
	* Edge版，每个月发行
* EE：企业版，收费。

## C03 使用Docker镜像
### 获取镜像
```
docke pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]
```

* 运行
```
$ docker run -it --rm ubuntu bash
```
	* -it ：这是两个参数，一个是-i ：交互式操作，一个是-t 终端。我们这里打算进入 bash 执行一些命令并查看返回结果，因此我们需要交互式终端。 
	* --rm ：这个参数是说容器退出后随之将其删除。默认情况下，为了排障需求，退出的容器并不会立即删除，除非手动 docker rm 。我们这里只是随便执行个命令，看看结果，不需要排障和保留结果，因此使用 --rm 可以避免浪费空间。

### 列出镜像
```
$ docker image ls

$ docker image ls -a

$ docker image ls ubuntu

$ docker image ls ubuntu:16.04

$ docker image ls -f dangling=true

$ docker image prune

$ docker system df

```

### 使用Dockerfile定制镜像
```
$ docker build -t nginx:v3
```

## C04 操作Docker容器

### 启动容器


## C05 Compose 简介
配置文件：docker-compose.yml

```
$ docker-compose --version
$ dokcer-compose up

```

## C06 Docker Machine项目


## C07 Docker Swarm项目


## C08 Swarm mode


## C09 安全


## C10 底层实现