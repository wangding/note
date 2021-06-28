# docker

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

# 使用阿里 docker 镜像，提高镜像拉取速度
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://v0yaxj7c.mirror.aliyuncs.com"]
}
EOF
systemctl daemon-reload
systemctl restart docker
```

## Docker 使用

```bash
# 查看本机镜像
docker images

# 拉取 centos 镜像
docker pull centos

# 搜索镜像
docker search tomcat

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
docker rm `docker ps -a -q`       # 模板字符串的引号里面可以是其他命令

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

--rm                      运行完容器后，删除容器
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

- MySQL  关系数据库，见 docker-demo 仓库的 05-mysql 分支
- nginx  静态 web 服务，见 docker-demo 仓库的 01-nginx 分支
- gogs   类似 github 的 git web 服务，见 docker-demo 仓库的 09-git 分支
- dozzle 查看 docker 容器日志的 web 服务，见 docker-demo 仓库的 08-log 分支
- nodejs Node.js 运行环境，见 docker-demo 仓库的 03-node 分支

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
