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
docker -h
docker images
docker pull centos
docker images
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://v0yaxj7c.mirror.aliyuncs.com"]
}
EOF
systemctl daemon-reload
systemctl restart docker
docker pull ubuntu
docker images
docker search tomcat
docker images
docker rmi ubuntu
docker images
docker run -it --name c1 centos /bin/bash
docker run -d --name c2 centos /bin/bash
history
docker ps
docker exec -it c1 /bin/bash
docker exec -it c2 /bin/bash
```
