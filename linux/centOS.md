# CentOS 作为开发和办公环境的安装过程

首先在虚拟机中构建 CentOS 办公环境，体验成功之后。再在物理机中安装使用 CentOS。下面的内容记录这个过程中的经验。

## 虚拟机创建

- 创建空的虚拟机  
- 操作系统版本：CentOS 64 位  
- 处理器数量 1 个，核心数量 2 个  
- 内存 2048  
- NAT 网络类型
- 磁盘类型默认
- 磁盘大小：20 G
- 将虚拟磁盘存储成单一文件

## 操作系统安装

安装的图形界面中，进行如下设置：

- 虚拟机设置 DVD 加载 CentOS ISO 镜像文件
- 启动虚拟机
- 第一个安装画面：选择安装 CentOS 7
- 语言：中文
- 安全策略：Common Profile for General-Purpose Systems
- 软件选择：开发及生成工作站，包括：图形生成工具，办公套件和生产效率
- 安装介质
- 安装位置
- 网络启用
- root 密码
- 创建新用户并设置密码，把新用户加到管理员组中

## 工作环境安装

- 安装 git 并验证 git 安装成功
```bash
sudo yum install git
git --version 
```
- 下载了 git 的配置文件，
  - 问题是如何能从网上一键安装配置文件？
  - git 的表现不完全和 windows 相同
- 火狐浏览器已经安装
- 设置火狐浏览器的参数
- 添加火狐浏览器的插件
  - vimperator
  - Adblock Plus
- 安装双拼输入
- 

## 常用命令

- ls -R 显示所有子目录和文件
- 查看 centOS 版本
```bash
cat /etc/redhat-release
```

## 常见问题

- 用户 sudo 不在 sudoers 用户组中的问题
http://blog.csdn.net/attagain/article/details/11987297


## 学习资料
http://billie66.github.io/TLCL/book/zh/index.html

## 腾讯主机控制台：
https://console.qcloud.com/cvm

## Linux 如何关机
```bash
# 1、执行命令“who”查看目前在线用户
who

# 2、执行命令“netstat -a”看网络的联机状态
netstat -a

# 3、执行命令“ps -aux”查看后台执行的程序
ps -aux

# 4、惯用的关机命令：shutdown
shutdown -h
# or
poweroff
```

## Linux 如何挂载 CD-ROM
```bash
# 确保 /mnt/ 目录下面有 cdrom/ 文件夹
mkdir /mnt/cdrom

# 挂载 CD-ROM
mount /dev/cdrom /mnt/cdrom
```
## yum 设置
```bash
# 设置从本地（虚拟机挂载的 iso 镜像）安装源安装软件
# 需要提前挂载 CD-ROM
# 并且禁用网络源，需要把 CentOS-Base.repo 文件改名为 CentOS-Base.repo.bak 

# yum 的配置文件分为两部分：main 和 repository
# main 部分定义了全局配置选项，整个yum 配置文件应该只有一个 main。常位于 /etc/yum.conf 中
# repository 部分定义了每个源/服务器的具体配置，可以有一到多个。常位于/etc/yum.repo.d 目录下的各文件中。
cd /etc/yum.repos.d/
ls

# 会看到四个 repo 文件，其中：
# CentOS-Base.repo 是yum 网络源的配置文件
# CentOS-Media.repo 是yum 本地源的配置文件
# 修改 CentOS-Media.repo
# 在 baseurl 中修改第 2 个路径为 /mnt/cdrom（即为光盘挂载点）
# 将 enabled=0 改为 1

# 运行 yum install 命令
yum install net-tools

# 设置国内的 yum 源（略），请参考文章：http://www.cnblogs.com/mchina/archive/2013/01/04/2842275.html
```

## 网络设置
```bash
vi /etc/sysconfig/network-scripts/ifcfg-eth0

# 地址是否自动获得 none 不自动获得，否则 dhcp 为自动获得
BOOTPROTO=dhcp
# 是否自动加载
ONBOOT=yes
```

## 启用 OpenSSH
参考：http://wangsheng1.blog.51cto.com/29473/1548853/

## 安装 vim
参考：http://www.jb51.net/os/RedHat/160662.html

## 安装 node.js
参考：https://nodejs.org/en/download/package-manager/#enterprise-linux-and-fedora
```bash
curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
yum -y install nodejs

# 检查 node.js 安装是否成功
node -v

# 检查 npm 是否安装成功
npm -v
```
## helloworld web 站点测试
【服务器端】node server.js
【客户端】http://192.168.59.130:1337

hello.js 代码如下：
```javascript
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World!\n');
}).listen(1337, '192.168.59.130');
console.log('Server running at http://192.168.59.130/');
```
## 开启 centOS 的防火墙端口
```bash
# 虚拟机本身可以打开页面
curl http://192.168.29.129:1337

# 宿主计算机的浏览器却不能打开页面
# 由此判断是 Linux 的防火墙没有打开端口

firewall-cmd --permanent --add-port=1337/tcp
firewall-cmd --reload
```
## 安装 selenium webdriver
参考：https://www.npmjs.com/package/selenium-webdriver
```bash
cd ~
mkdir selenium
cd selenium

# 安装 Selenium webdriver
npm install selenium-webdriver
# 检查模块文件夹是否存在
ls
```

## 安装 phantomJS
http://www.cnblogs.com/LH2014/p/4073881.html
```bash
# 安装依赖软件
yum -y install wget fontconfig

# 下载安装包
wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2

# 解压缩
tar jxvf phantomjs-2.1.1-linux-x86_64.tar.bz2

# 移动位置
mv phantomjs-2.1.1-linux-x86_64 /usr/local/src/phantomjs

# 建立软连接
ln -sf /usr/local/src/phantomjs/bin/phantomjs /usr/local/bin/phantomjs
```

## Selenium + Phantomjs 的测试代码
貌似好像跑通了
```javascript
var webdriver = require('selenium-webdriver'),
    By = webdriver.By,
    until = webdriver.until;

var driver = new webdriver.Builder()
    .forBrowser('phantomjs')
    .build();

driver.get('http://www.baidu.com');
driver.findElement(By.id('kw')).sendKeys('selenium');
driver.findElement(By.id('su')).click();
driver.wait(until.titleIs('selenium_百度搜索'), 1000);
console.log('OK!');
driver.quit();
```
## 网页按钮推动后台操作<待续>

## node.js 代码开发的工具有待研究
