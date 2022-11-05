# docker

## Docker 概述

### Docker 是什么

- Docker 不是编程语言
- Docker 不是软件架构
- Docker 不是虚拟机，是 Linux 上的工具软件。Docker 的开销比虚拟机小。
- Docker 是一套工具软件，包括：命令行，服务程序和一组远程服务。
- Docker 解决常见的软件问题：安装、运行、发布和删除。

### Docker 基本概念

- Docker 提供隔离的环境让软件运行其中，这个隔离的环境就是容器。
- Docker 提供软件发布的方式，发布的形式是镜像。
- 传统的软件发布方式是源代码或者二进制可执行程序，基于 Docker 的软件发布方式是镜像。
- 传统的软件构建是生成可执行的二进制程序，基于 Docker 的软件构建是构建镜像。
- travis-ci 构建镜像，并发布到 docker hub 上，见：docker-demo 的 12-travis-ci 分支。
- 镜像相当于软件包，包含软件以及软件运行的环境（依赖）。
- 启动镜像（本地没有镜像，会自动拉取），软件即可使用。免去了软件的安装，以及依赖的安装过程
- 容器是镜像运行时的形态。
- 容器是 Docker 服务程序的子进程，每个子进程只能访问自己的内存空间和资源。形成了隔离的运行环境，就是容器，好比是一个一个的罐头瓶。
- Docker 英文单词是码头工人，码头工人在码头装卸集装箱。Docker 镜像或容器，好比集装箱。集装箱里的东西，就是软件及其运行环境（依赖）。所有软件及其依赖使用起来，各不相同。但是一旦放到集装箱里面了（封装成镜像或容器后），操作方式就相同了。
- 从这个角度来看，docker 提供了一层抽象，以后安装任何软件，操作方式都相同了，都是操作镜像。
- 容器技术的底层是 Linux 命名空间和 cgroups。Docker 不提供容器技术，但是它使得容器更易于使用。
- cgroups 是 2007 年出现的技术，docker 是 2013 年出现的技术。
- 容器的运行状态跟容器内单次运行的程序状态相关联。如果程序运行，则容器运行；如果程序退出，则容器退出。
- Docker 可以运行在 Linux, OS X 和 Windows 上，因此镜像软件可以运行在任何操作系统上，Docker 提供了软件的可移植性。

### linux 内核的两大隔离手段

- 命名空间（name space）用来产生隔离，可以解决资源冲突问题。例如：web-app-a 监听 80 端口和 web-app-b 监听 80 端口，就会冲突。而隔离的 NET 命名空间，两个 app 所在的容器，有各自独立的 IP 地址，就解决了端口冲突问题。
- ns: name space，命名空间，提供各种资源的隔离，共有以下六种：
  - PID 命名空间——进程标识符，提供进程隔离
  - UTS 命名空间——主机名和域名，提供主机名隔离（UTS：UNIX Time-sharing System）
  - MNT 命名空间——文件系统访问，提供磁盘挂载点和文件系统隔离
  - IPC 命名空间——共享内存的进程间通信，提供进程间通信隔离
  - NET 命名空间——网络访问，提供网络隔离
  - USR 命名空间——用户名标识，提供用户隔离
- cgroups——资源保护，实现访问控制

其他：
- chroot() ——文件系统根目录，比较早的技术，跟 MNT 命名空间功能类似

### 容器进程系统抽象和隔离

- pid 是 process id，进程的唯一标识。
- pid 命名空间会包含自己的 pid1, pid2，...
- 为每个容器创建一个独立的 PID 空间，是 Docker 隔离操作的一个方面。
- `--pid host` 容器使用宿主的 PID 空间，不使用隔离的 PID 命名空间。
- 这个功能不是重点，默认正常使用就行，不用特殊设置和调整。

### 镜像层

- 镜像是分层的，镜像实际是镜像层的集合。
- 一个镜像层至少和一个其他镜像关联。
- 分层之间是有依赖关系的，顶层依赖与底层，或者子层依赖于父层。
- 假设 node-app-a 和 node-app-b 两个镜像都依赖基础镜像 nodejs:alpine。安装 node-app-a 镜像时，会安装基础镜像以及 node-app-a 的镜像层。安装 node-app-b 时，基础镜像本地已经有了，则只下载安装 node-app-b 镜像层。这样会提高镜像下载和安装的速度。
- 公共层只需要下载安装一次。
- 分层提供了用于依赖管理和隔离的工具。通过检查镜像和分层可以识别每层安装的软件。
- 只要在某些基础镜像上，做一些稍微的变化，就可以方便的构建新的镜像软件，这个过程就是在一层一层的搭积木。

### 容器文件系统抽象和隔离

- 容器中正在运行的程序对镜像分层一无所知，仿佛操作不是发生在容器中或者镜像层上。
- 从容器的角度看，它具有由镜像层所提供文件的独占副本，这就是所谓的 union 文件系统。
- Docker 支持多种 union 文件系统，并给出适合你的最佳选择。
- union 文件系统是创建有效文件系统隔离极为关键的一套工具，其他工具还有 MNT 命名空间和 chroot 系统调用。
- chroot 是 change root，用来改变根目录的挂载点，可以把某个目录挂载为根路径，这个技术很早就有了。
- mnt 可以为某进程设置某目录为根挂载点，形成文件系统的抽象和隔离。
- union 文件系统使用写时复制的模式，使得内存映射文件（mmap 的系统调用）的实现比较困难。
- 容器的目录树是由一组挂载点创建而成，这些挂载点描述了如何构建出一个或多个文件系统。
- 存储卷是容器目录树上的挂载点。
- union 文件系统适用于创建和分享镜像，但对持久化或共享数据，并不是理想的方法，存储卷能很好的解决这些问题。
- 存储卷提供与容器无关的数据管理方式。
- 容器的文件系统分两大类：镜像分层 union 文件系统（生命周期跟着容器）和存储卷（生命周期脱离容器）。
- 镜像分层适合打包和分发相对静态的文件，例如：程序源代码或者可执行程序。
- 存储卷适合管理程序运行时，动态产生的数据。

### 存储卷的类型

- 存储卷的生命周期独立于被挂载到的容器。
- 存储卷有两种类型，bind 存储卷和 volume 存储卷。
- 挂载 bind 存储卷，docker 命令参数：`-v 主机路径:容器路径`。
- bind 存储卷使用用户提供的目录或文件，注意，上面的 `-v` 参数，不论主机路径还是容器路径，都是绝对路径。
- volume 存储卷由 Docker 服务程序管理的特定目录，路径是：`/var/lib/docker/volumes/<cid>/_data`。
- 挂载 volume 存储卷，docker 命令参数：`-v 容器路径`，不用指定主机路径，注意，容器路径是绝对路径。
- bind 存储卷可以在容器和主机之间共享数据，例如：开发网站静态页面，将项目目录挂载到 nginx 容器网站根路径，对于 nginx:alpine 镜像这个路径是 `/usr/share/nginx/html/`。
- 只读 bind 存储卷，`-v 主机路径：容器路径:ro`。只读 bind 存储卷，容器中的程序不能修改，存储卷中的内容。
- bind 存储卷，不止可以挂载目录，也可以挂载文件。volume 存储卷只能挂载目录。
- bind 存储卷，可以挂载主机的任何路径。volume 存储卷只能挂载 docker 管理的路径，挂载时不能指定要挂载的主机路径。
- 多个同一镜像的容器，都使用相同的 bind 存储卷，挂载到相同的主机目录，可能会导致冲突。volume 存储卷就不会发生这样的问题。
- volume 存储卷使用和管理的成本更低。`docker system df -v` 可以检查存储卷占用的空间，`docker volume` 可以删除无用的 volume 存储卷。
- 删除容器时 `docker rm -v <cid>`，`-v` 参数可以一并将该容器挂载的 volume 存储卷一并删除。所以，volume 卷的维护成本低。
- 如果删除容器时，没有使用 `-v` 参数，则这个容器之前挂载的 volume 卷就成了孤立卷。孤立卷会逐步蚕食 docker 存储空间，最终将导致存储空间不足。
- 宿主机和容器之间共享数据，使用 bind 存储卷和 volume 存储卷都可以。
- 容器和容器之间共享文件，有两种方案：
  - 使用 bind 存储卷，多个容器挂载到同一个主机目录。注意，当容器过多时，同时操作相同的文件可能会出问题。读写分离的容器可能问题会好很多，例如：一个容器负责写数据，一个容器负责读数据，问题不大。如果两个以上的容器都要写数据，就会导致冲突发生。
  - 使用存储卷容器，其他容器使用 `--volume-from <cid or cnm>` 链接到存储容器上。一个容器可以 `--volume-from` 多个存储容器。
- 容器和容器之间共享数据的方案，最好是使用数据库容器，多个应用容器连接到数据库容器。
- `--volumes-from` 会将存储容器中挂载的卷（无论哪种类型），复制到目标容器中。复制卷总是具有相同的挂载点。复制卷不能修改卷的读写模式。
- 卷容器，是一个容器，只提供卷的句柄。卷容器不需要运行，因为停止的卷容器仍能保证存储卷的引用。卷容器一般使用 volume 存储卷，而不使用 bind 存储卷。
- 数据打包的存储卷容器，是卷容器的一种用法。利用容器将镜像中的静态资源，复制到其挂载的存储卷中。这个存储卷通过 `--volumes-from` 与其他目标容器之间，实现数据分发。通常用于分发的数据可能是：关键架构信息，如：配置、密钥或代码，等。
- 多态工具是以一致性的方式进行交互，但可能有多个实现，分别做不同的事情。使用存储卷，你可以注入不同的行为到容器中，而无需修改其镜像。

### 常见的资源冲突

- 两个程序监听相同的端口号。
- 两个程序使用相同的临时文件名和文件锁。
- 两个程序使用不同版本且全局安装的库。
- 同一个程序的两个副本使用相同的 PID 文件。
- 第二个程序修改了，第一个程序正在使用的环境变量，导致导致第一个程序崩溃。
- 命名空间和 cgroup 手段提供隔离措施，可以避免冲突的发生。

### 容器名称

- 启动同一个镜像的多个容器，容器名称可能会冲突。
- 不指定容器名称时，docker 会自动分配名称。
- 当然，每个容器有唯一的 ID，可以标识该容器，称为 CID。
- 因为，容器启动（docker run）和创建（docker create），都会返回 CID。
- 所以，CID 可以方便的用脚本处理，例如:  

```bash
#!/bin/sh

$MAILER_CID=$(docker run -d dockerinaction/ch2_mailer)

# 这里如果需要创建 1000 个 web + agent 的农场，只要写个 for 循环
$WEB_CID=$(docker run -d nginx:alpine)
$AGENT_CID=$(docker run -d --link $MAILER_CID:insidemailer --link $WEB_CID:insideweb dockerinaction/ch2_agent)
```

- 或者，使用如下的快捷命令：

```bash
docker stop $(docker ps -aq)   # 停止所有容器
docker rm $(docker ps -aq)     # 删除所有容器
```

### 建立与环境无关的系统

- 只读文件系统，容器不能更改它包含的文件，这样攻击者不能对容器造成破坏，使用 `--read-only`。
- 环境变量注入
- 存储卷

### Docker 容器的四个状态

- 运行
- 已暂停
- 重新启动
- 已退出（包括：容器尚未启动）

### 软件分发（镜像的来源）

- Docker Hub（开源，免费）
- 私有镜像服务器（闭源）
- 从文件加载镜像
  - `docker save -o myfile.tar busybox:latest`，把镜像导出成本地文件，`-o, output`
  - `docker load -i myfile.tar`，从本地文件载入镜像，`-i, input`
- 从其他来源下载
  - 例如：`docker pull quay.io/dockerination/ch3_hello_registry:latest`
  - 需要在镜像的名称前面加上服务器的地址
- 使用 Dockerfile 构建镜像
  - Dockerfile 一般通过 GitHub 分发
  - Dockerfile 是描述镜像构建步骤的脚本
  - `docker build . -t hello-docker:latest --rm=true`

### Docker 网络

- 容器有以下四种网络模型，提供不同的隔离程度，容器的网络模型只属于其中之一：
  - closed，没有网络，完全隔离，容器内不能访问互联网。容器外不能通过网络访问容器内。使用参数 `--net none` 创建。应用场景：运行 node.js 命令行程序的容器。
  - bridged，桥接，默认的网络模型。每个容器拥有一个本地回环接口（127.0.0.1）和一个单独的以太网接口（172.17.xxx.xxx），这个以太网接口跟主机的 172.17.xxx.1 接口连接。容器内可以访问外部网络，外部可以访问容器内网络。
  - joined。如果需要在不同容器上的程序通过本地回环接口进行通信时，使用 joined 容器。joined 容器之间共享一个网络栈，容器之间没有网络隔离。使用参数 `--net container:<cid>`。
  - opened，没有网络隔离，容器在宿主的网络中。没有单独的 IP 地址。容器中的服务程序，直接跑在主机的网络环境中。使用参数 `--net host` 创建。应用场景：云主机上的 nginx 反向代理容器。
- 上面四种网络模型的隔离程度，从上到下，隔离程度逐次降低。

### Docker Compose

- Docker Compose 是一个用于定义、启动和管理服务的工具。
- 在 YAML 文件中定义了服务和服务系统，并通过命令行 docker-compose 进行管理。
- Docker Compse 是描述完整的环境以及服务组件的交互。
- 一个 Compose 文件可能会描述四到五个独立的服务，它们之间是相关关联的，应保持隔离和独立的伸缩。

## Docker 安装

Docker 分两个版本，docker-ce(Community Edition) 和 docker-ee(Enterprise Edition)。CE 版本是免费的、社区版。

具体安装步骤，参考 Docker 官方文档：https://docs.docker.com/engine/install/centos/

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo yum list docker-ce --showduplicates | sort -r
sudo systemctl start docker
sudo systemctl status docker
sudo systemctl enable docker
docker version
```

## Docker 配置

```bash
# 以非 root 用户身份使用 docker
sudo usermod -aG docker $USER   # $USER 是当前登录的用户
                                # 此命令执行后，需注销，重新登录，才生效

# 使用国内 docker 镜像，提高镜像拉取速度
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": [
    "https://mirror.ccs.tencentyun.com",
    "http://hub-mirror.c.163.com",
    "https://registry.docker-cn.com",
    "http://f1361db2.m.daocloud.io",
    "https://v0yaxj7c.mirror.aliyuncs.com",
    "https://05f073ad3c0010ea0f4bc00b7105ec20.mirror.swr.myhuaweicloud.com"
  ]
}
EOF
systemctl daemon-reload
systemctl restart docker
```

## Docker 使用（常用操作）

```bash
# 查看本机镜像
docker images

# 删除镜像
docker rmi ubuntu

# 运行交互式容器
docker run -it --name c1 centos /bin/bash

# 运行守护式容器
docker run -d --name c2 centos

# 查看容器运行的日志
docker logs c1

# 重启容器
docker restart c2

# 停止容器
docker stop c1

# 删除容器，前提容器不能是运行状态
docker rm c2
docker rm `docker ps -a -l`       # 模板字符串的引号里面可以是其他命令
docker rm $(docker ps -a -l)      # 跟上面的操作等价

# 在容器中执行命令
docker exec -it c1 /bin/bash
docker exec -it c2 /bin/bash

# 检查容器详细信息
docker inspect c2

# 修改容器的名称
docker rename old-name new-name

# 容器和宿主机之间的文件复制
# src 是源，dst 是目的地
# 容器中的内容，容器名称:文件路径或文件夹路径，例如，c2:/src/a.txt
# dst 一般是文件夹路径
docker cp src dst

# 创建容器，但不运行
docker create centos

# 查看运行的容器
docker ps

# 删除所有容器，前提是这些容器已经暂停运行
docker rm $(docker ps -aq)
docker ps -a | awk 'NR>1 {print $1}' | xargs docker rm

# 目录挂载，注意宿主目录和容器目录必须是绝对路径
docker -d --name c2 -v 宿主机目录:容器目录 镜像名字

# 检查容器元数据，检查容器是否运行
docker inspect --format "{{.State.Running}}" c1
docker inspect -f "{{.State.Running}}" c1

# 常用参数
--link 容器名字：别名     链接到某个容器，解决主机名到 IP 地址映射的问题
                          链接时静态的，不传递的
                          链接目标的容器必须先启动
                          新容器中会创建环境变量来保存目标容器的名称和 IP Addr

--rm                      运行完容器后，自动删除容器
-e 环境变量=值            设置容器的环境变量，-e = --env
--pid host                没有 PID 隔离的容器（一般不这样做）
--cidfile 容器名称文件    把容器的 ID，保存到容器名称文件中，应该给出绝对路径
docker ps -l -q           返回最后创建容器的截断的 ID
-l = --latest
-q = --quiet
docker ps --no-trunc      返回
-f = --format
-v = --volume
-p 宿主端口:容器端口      把容器端口映射到主机端口
-p <container port>
-p <hostport>:<container port>
-p <hostip>:<hostport>:<container port>
--read-only               只读文件系统
--restart

# 搜索镜像，一般回到 Docker Hub 网站搜索
docker search tomcat

# 拉取 centos 镜像，本操作可以跳过，可以直接启动镜像
# 当本地没有要启动的镜像时，会自动拉取
docker pull centos
```

## Docker 空间清理

```bash
# 查看磁盘空间占用，包括：镜像、容器、卷和缓存
docker system df -v

# 清理
docker system prune

# 深度清理
docker system prune -a

# 清理无用的卷
docker volume rm $(docker volume ls -qf dangling=true)
```

## 创建镜像

```bash
# 构建镜像
docker build -t 镜像的名字 --rm=true .
# --rm=true 删除中间镜像
# . 表示用当前目录的 Dockerfile 来创建镜像

# Dockerile 基于 DSL（Domain Specific Language） 语法

# 设置镜像 tag
docker tag

# 登录镜像仓库网站
docker login

# 推送镜像
docker push
```

## 容器管理

```bash
# 安装 Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 添加运行权限
sudo chmod +x /usr/local/bin/docker-compose

# 检查是否安装成功
docker-compose --version

# 使用 Docker Compose
# 例如，bitnami redmine: https://hub.docker.com/r/bitnami/redmine
```

## 快速上手：nginx + 静态站

操作如下：
- 以下所有操作在 CentOS 7 控制台下完成。
- 安装 Docker，参考下面的文档。如已安装 Docker，跳过此步。
- 配置 Docker 环境，参考下面的文档。包括：非 root 用户使用 Docker，以及 Docker 阿里镜像。如已配置，跳过此步。
- 创建 `hello-docker` 目录，并进入该目录。运行命令：`mkdir hello-docker && cd hello-docker`
- 创建 `index.html` 文件，内容为 `<h1>hello world</h1>`。运行命令：`echo "<h1>hello world</h1>" > index.html`
- 创建 `Dockerfile` 文件，文件内容如下。
```
FROM nginx:alpine
COPY ./index.html /usr/share/nginx/html/index.html
EXPOSE 80
```
- 打包镜像。运行命令：`docker build . -t hello-docker:1.0.0 --rm=true`
- 查看镜像。运行命令：`docker images`
- 运行容器。运行命令：`docker run -d --name hello -p 8080:80 hello-docker:1.0.0`
- 查看容器。运行命令：`docker ps`
- 访问静态站。运行命令：`curl http://localhost:8080`

注意：
- linux 上 8080 端口不要占用
- linux 上 8080 端口防火墙打开，可以通过浏览器来访问：`http://<linux-ip-addr>:8080`
- 如果网站静态资源都在 `./dist` 目录下，则 `Dockerfile` 的内容如下：
```
FROM nginx:alpine
COPY ./dist/ /usr/share/nginx/html/
EXPOSE 80
```

## 镜像瘦身

1. 瘦身技巧 1：用 alpine 版本的镜像  
alpine 是一个常用的 Docker 基础镜像。Alpine 操作系统是一个面向安全的轻型 Linux 发行版。它不同于通常 Linux 发行版，Alpine 采用了 musl libc 和 busybox 以减小系统的体积和运行时资源消耗，但功能上比 busybox 又完善的多，因此得到开源社区越来越多的青睐。

2. 瘦身技巧 2：合并指令  
一个Docker 镜像的尺寸是每一个独立镜像层的尺寸之和，这也就是联合文件系统的工作机制。这里并不存在“负”的镜像层尺寸。于是，Dockerfile 中每一个指令要么保持镜像尺寸不变，要么增加它的尺寸。同时，每一步还会引入新的元数据信息，使得整体尺寸在增大。为了降低整个镜像的尺寸，清除操作应该在同一镜像层中执行。于是，解决方案是将先前的多条指令合并成一条。当Docker 使用/bin/sh 来执行每一条指令时，我们可以使用Bourne shell 提供的&&操作符来实现链接。

例如：
```
FROM debian:jessie

RUN echo deb http://httpredir.debian.org/debian\
         jessie-backports main\
         > /ect/apt/sources.list.d/jessie-backports.list
RUN apt-get update && \
    apt-get --no-install-recommends \
            install -y opendjdk-8-jre-headless && \
    rm -rfv /var/lib/apt/lists/*
```

## 常用软件

- apline，最轻量的 linux 基础镜像。
- MySQL，关系数据库，见 docker-demo 仓库的 05-mysql 分支
- nginx，静态 web 服务，见 docker-demo 仓库的 01-nginx 分支
- gogs，类似 github 的 git web 服务，见 docker-demo 仓库的 09-git 分支
- dozzle，查看 docker 容器日志的 web 服务，见 docker-demo 仓库的 08-log 分支
- nodejs，Node.js 运行环境，见 docker-demo 仓库的 03-node 分支
- redmine，项目管理平台，见 docker-demo 仓库的 10-redmine 分支
- wordpress，博客网站或企业网站，见 docker-demo 仓库的 1
- gcc，C 语言编译器及运行环境，见 docker-demo 仓库的 11-gcc 分支

## 其他

```bash
# 搭建私有镜像仓库
docker run -d -p 5000:5000 --restart=always --name registry \
-v /home/wangding:/var/lib/registry registry:latest

docker tag hello-world:latest localhost:5000/hello-world:1.0.0

docker push localhost:5000/hello-world:1.0.0

# 通过浏览器查看仓库信息
http://192.168.133.144:5000/v2/hello-world/tags/list

# 通过磁盘文件查看仓库信息
ls /home/wangding/docker
```
