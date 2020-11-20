# docker

## Docker 安装

Docker 分两个版本，docker-ce(Community Edition) 和 docker-ee(Enterprise Edition)。CE 版本是免费的、社区版。

具体安装步骤，参考 Docker 官方文档：https://docs.docker.com/engine/install/centos/

```bash
yum install -y yum-utils
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce docker-ce-cli containerd.io
yum list docker-ce --showduplicates | sort -r
systemctl start docker
systemctl status docker
systemctl enable docker
docker version
docker run hello-world
```

## Docker 使用

```bash
# 查看 docker 帮助
docker -h

# 查看本机镜像
docker images

# 拉取 centos 镜像
docker pull centos

# 使用阿里 docker 镜像，提高镜像拉取速度
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://v0yaxj7c.mirror.aliyuncs.com"]
}
EOF
systemctl daemon-reload
systemctl restart docker

# 搜索镜像
docker search tomcat

# 删除镜像
docker rmi ubuntu

# 运行交互式容器
docker run -it --name c1 centos /bin/bash

# 运行守护式容器
docker run -d --name c2 centos /bin/bash

# 重启容器
docker restart c2

# 停止容器
docker stop c1

# 查看容器运行的日志
docker logs c1

# 修改容器的名称
docker rename old-name new-name

# 创建容器，但不运行
docker create centos

# 查看运行的容器
docker ps

# 在容器中执行命令
docker exec -it c1 /bin/bash
docker exec -it c2 /bin/bash

# 检查容器元数据，检查容器是否运行
docker inspect --format "{{.State.Running}}" c1

# 常用参数
--link 容器名字：别名     链接到某个容器
-e 环境变量=值            设置容器的环境变量
--pid host                没有 PID 隔离的容器（一般不这样做）
--cidfile 容器名称文件    把容器的 ID，保存到容器名称文件中，应该给出绝对路径
docker ps -l -q           返回最后创建容器的截断的 ID
-l = --latest
-q = --quiet
docker ps --no-trunc      返回
```
