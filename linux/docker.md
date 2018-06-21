# docker

## 目标

- 用 Docker 实现 Node.js 开发环境
- 用 Docker 实现 Node.js 程序的测试和评价

## Docker 安装

### 一、查看内核是否符合要求

| CentOS版本 | 内核版本 |
| ---------- | -------- |
| CentOS 7 x64 | 3.10 以上 |
| CentOS 6.5+ x64 |  2.6.32-431 以上 |

查看内核版本，使用下面的命令：

```bash
$ uname -r
```

### 二、安装

安装最新版本的 Docker。最新版本的 Docker 分两个版本，docker-ce(Community Edition)和docker-ee(Enterprise Edition)。CE 版本是免费的、社区版。

1 安装依赖的软件包

```bash
$ sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

2 设置稳定版仓库

# 添加官方数据源

```bash
$ sudo yum-config-manager \
  --add-repo \
  https://download.docker.com/linux/centos/docker-ce.repo

# 添加阿里云数据源
$ sudo yum-config-manager \
  --add-repo \
  https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

3 安装

```bash
$ sudo yum install -y docker-ce # 安装最新版本
```

4 启动Docker

```bash
$ sudo systemctl start docker # 启动
$ sudo systemctl stop docker
$ sudo systemctl restart docker

$ sudo docker run hello-world # 检查 docker 运行正常
```

5 检查 docker 是否安装成功

$ docker --version # 查看安装的 docker 版本
