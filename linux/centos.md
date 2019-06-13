# CentOS

## CentOS 作为开发和办公环境的安装过程

首先在虚拟机中构建 CentOS 办公环境，体验成功之后。再在物理机中安装使用 CentOS。下面的内容记录这个过程中的经验。

### 创建虚拟机

- 创建空的虚拟机  
- 操作系统版本：CentOS 64 位  
- 处理器数量 1 个，核心数量 2 个  
- 内存 2048  
- NAT 网络类型
- 磁盘类型默认
- 磁盘大小：20 G
- 将虚拟磁盘存储成单一文件

### 安装操作系统

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

### 安装工作环境

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
- 配置 ibus 的双拼输入

## 常用命令

- ls -R 显示所有子目录和文件
- 查看 centOS 版本
```bash
cat /etc/redhat-release
```
- rpm -aq 查看本机安装的软件包
- init 3 从窗口界面进入命令行界面
- init 5 或 startx 从命令行界面进入窗口界面
- nmtui 命令行界面设置网卡
  - 在 root 权限下设置 NAT 模式下固定 IP 地址
  - 用 nmtui 设置网卡的 IP 地址、子网掩码、DNS，等
  - 例如：192.168.29.144/24
  - 默认网关是 x.x.x.2
  - vim 修改 /etc/sysconfig/network-scripts/ifcfg-ensxx（查 ifconfig 知道网卡的名字）
  - BOOTPROTO=static
  - systemctl restart network # 让修改的 IP 地址立刻生效

- ps -ef 查看系统中的进程
- which firewalld 查看进程 firewalld 用到的命令
- kill pid 杀掉 pid 的进程
- kill -9 970 强制删除 970 进程
- gsettings set org.gnome.desktop.interface cursor-blink false 设置终端光标不闪烁
- passwd wangding 修改当前用户 wangding 账户的密码
- sudo hostnamectl --static set-hostname DEV 设置主机名为 DEV
- hostnamectl status 查看主机名信息


## 安装卸载程序（yum 包管理）

- yum list 列出已安装的和可安装的应用程序包
- yum list package 列出 package 应用的安装情况
- yum clean 清除缓存的软件包信息
- /etc/yum.repos.d/\*.repo  yum 源定义文件
- 把 cdrom 的安装包设为本地 yum 源
- yum install package 安装 package
- yum remove package 删除 package
- yum update package 升级 package
- yum list updates 列出所有可以升级的软件包

## 启动服务

- systemctl start mariadb  启动 mariadb 数据库服务
- systemctl start httpd    启动 apache 服务
- systemctl status httpd   查询 apache 服务是否启动
- systemctl restart httpd  重新启动 apache 服务
- apache 服务启动不正常的解决办法
  firewall-cmd --add-service=http

## 用户、组和文件权限

- useradd wangding 添加新用户 wangding
- vipw 命令查看系统中的用户，一般新添加的用户都在文件的最后一行
  查看的信息包括：用户 ID 和主 ID，用户家目录，用户的 shell
- groupadd abc 添加 abc 用户组
- vigr 命令查看用户组的信息，vipw 命令和 vigr 命令是有规律的，vi 代表 vi 编辑器，其实是用 vi 编辑器查看信息的。pw 代表 password 用户，gr 代表 group 用户组。查看的信息包括：组的 ID 和组的成员。
- gpasswd -a username groupname 把用户加到组中
- groups wangding 查看用户 wangding 所在的用户组信息
- whoami 查看当前登录的用户
- su - 切换到 root 用户，su 是 switch user 的缩写
- su - wangding 将当前用户环境切换到 wangding 用户环境下面，退出用 exit
- userdel wangding 删除用户 wangding
- groupdel 删除组
- id root 查看 root 用户的 ID 值，ID 值越小权限越大
- chmod permission filename 修改文件权限
- permission：r=4, w=2, x=1, rw=4+2=6, rx=4+1=5, 等等，用户权限，组权限和其他用户权限，按顺序依次为三个组
- chown user filename 改变文件或目录的所有者，ch: change, own：owner
- chgrp group filename 改变文件或目录的组名
- chown user.group filename 改变文件或目录的所有者为 group 组的 user 用户

## 常见问题

- 用户 sudo 不在 sudoers 用户组中的问题
http://blog.csdn.net/attagain/article/details/11987297

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

# 运行 yum install 命令，net-tools 安装包中包括 ifconfig 命令
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
curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
sudo yum -y install nodejs

# 检查 node.js 安装是否成功
node -v

# 检查 npm 是否安装成功
npm -v
```
## helloworld web 站点测试

【服务器端】node server.js
【客户端】`http://192.168.59.130:1337`

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
sudo firewall-cmd --zone=public --list-ports
# 上面的命令列出本机防火墙打开的所有端口
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
yum install -y wget fontconfig

# 下载安装包
wget -c https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2

# 解压缩
tar jxvf phantomjs-2.1.1-linux-x86_64.tar.bz2

如果 tar 出错，错误信息是：tar (child): bzip2：无法 exec: 没有那个文件或目录
则说明没有安装 bzip2
yum intall -y bzip2

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

## 字体美化

- http://www.jinbuguo.com/gui/fonts.conf.html

## zsh

zsh 的安装过程如下：

- echo $SHELL                   # 查看当前的 shell
- sudo yum install -y zsh       # 安装 zsh
- sudo yum install -y wget      # 安装 wget
- wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
- vim ~/.zshrc                  # 编辑 zsh 的配置文件
- chsh -s /bin/zsh              # 却换 bash 至 zsh
- exit                          # 查新登录 shell

## tmux

tmux 的安装和使用：

- sudo yum install -y libevent-devel ncurses-devel
- sudo yum install -y tmux
- tmux
- 一堆快捷键，请参考：http://blog.csdn.net/hcx25909/article/details/7602935
    http://cenalulu.github.io/linux/tmux/

## strace 的用法

- 安装：yum install -y strace
- 使用：
```bash
ls xxx
strace -eopen ls
```

## locale 的用法

- 参考资料：
http://blog.chinaunix.net/uid-20726500-id-4662320.html

## nfs 的用法


## 通过 xshell windows 给 linux 虚拟机上传文件

http://www.linuxidc.com/Linux/2015-05/117975.htm

## linux 查找文件内容

```bash
grep "hello" ./*.js  # 在当前目录的所有 js 文件中查找 hello 字符串
```

## 命令行快捷键

快捷键大全的参考资料，非常权威：
- https://linux.cn/article-5660-1.html

- ctrl + a 移动光标到行首  ahead  
- ctrl + e 移动光标到行尾  end

- ctrl + f 按字符前移（右） forward  
- ctrl + b 按字符后移（左） backward  
- alt  + f 按单词前移（右） forward  
- alt  + b 按单词后移（左） backward  

- ctrl + w 删除光标前面的一个单词  
- alt  + d 删除光标后面的一个单词

- ctrl + k 从光标处删除至命令行尾  
- ctrl + u 从光标处删除至命令行首  

- ctrl + r 逆向搜索命令历史  
- ctrl + d 删除当前字符
- ctrl + h 删除光标前一个字符

- ctrl + l 窗口清屏，效果等同命令 clear  

- alt  + c 从光标处更改为首字符大写的单词 capital  
- alt  + u 从光标处更改为全部大写的单词   upper  
- alt  + l 从光标处更改为全部小写的单词   lower  

- ctrl + t 交换光标处和之前的字符
- alt  + t 交换光标处和之前的单词


在 xshell 中使用 alt 快捷键，需要进行设置，否则会和 window 窗口的快捷键冲突：

## 搭建 apache 服务器

```bash
# 安装软件
sudo yum install -y httpd

# 开通端口
sudo firewall-cmd --add-service=http
sudo firewall-cmd --permanent --add-port=80/tcp
sudo firewall-cmd --reload

# 启动服务
systemctl enable httpd.service
systemctl start httpd.service

# 浏览器测试，应该能看到测试网页
http://ip_addr/

# 配置 apache，编辑 /etc/httpd/conf/httpd.conf 配置文件
```

## 搭建 lighttpd 服务器

```bash
# 安装文件
sudo yum install -y epel-release
sudo yum update
sudo yum install -y lighttpd, gitweb

# lighttpd 是 web 服务器，gitweb 是网站代码，或者网站程序
```

export 命令的用法

1、执行脚本时是在一个子shell环境运行的，脚本执行完后该子shell自动退出；
2、一个shell中的系统环境变量才会被复制到子shell中（用export定义的变量）；
3、一个shell中的系统环境变量只对该shell或者它的子shell有效，该shell结束时变量消失（并不能返回到父shell中）。
4、不用export定义的变量只对该shell有效，对子shell也是无效的。

```bash
# 实验，验证 export 命令的用法

test='hello'
echo $test

vi a.sh

# --- 以下是 a.sh 中的内容

#!/usr/bin/sh

echo $PATH
echo $test

# --- a.sh 内容结束

chmod u+x a.sh

./a.sh

# 看不到 test 变量的值

export test
./a.sh

# 可以看到 test 变量的值
```

## crontab 定时任务

【参考资料】  
- https://www.cnblogs.com/peida/archive/2013/01/08/2850483.html

```bash
sudo crontab -e -u wangding   # -e 编辑某个用户的 crontab，如果不指定用户，则编辑当前用户的 crontab 文件，-u user 用来设定某个用户的 crontab 服务
sudo crontab -l -u wangding   # 查看某个用户的 crontab 文件内容
sudo crontab -r -u wangding   # 删除某个用户的 crontab 文件内容
```

crontab 文件的内容
```
*      *  *   *    *     command
# 分钟 小时 日 月 星期几
```
特殊符号：
\*: 代表说有可能值
, : 代表一个列表范围，例如：1, 3, 5, 7
- : 代表一个整数范围，例如：2-6，表示 2, 3, 4, 5, 6
/ : 代表指定时间的间隔频率：例如：\*/2 在分钟位置，每隔两分钟执行一次 

查看 crontab 日志，来排错：
排错的另一个经验，可以先在特定目录下，执行 crontab 中的命令，目录最好都用绝对路径，命令执行成功之后，再考虑定时执行。

```bash
cd /var/log
sudo less /var/log/cron.log
```

## curl 常用参数

- GET 请求 URL：`curl http://localhost:8080`
- POST 请求 URL：`curl -X POST http://localhost:8080 -d "item=abc"`
- curl 默认请求方法是 GET，修改请求方法的参数是 -X，例如：`curl -X PUT http://localhost:8080`
- curl 的 -v 参数，除了可以看到响应体，还可以看到请求头和响应头，当然 curl -i 参数可以看到响应头的，-v 参数打印信息的时候，请求头和响应头前面的前导符号是大于号和小于号，正好相反，反映了数据发送的两个方向，设计的很细腻。
- curl -H 参数可以定制请求头信息，例如：`curl -H "Content-Type:appliction/json" http://localhost:8080`，如果需要多个自定义的头字段，就多加几个 -H 参数，一个 -H 参数跟一个头字段信息
- 综合起来，curl POST 发送 JSON 数据的命令：例如：`curl -H "Content-Type:application/json" -X POST -d '{"name":"wangding","age":"41"}'`
- curl -F 参数可以上传文件，参数格式：-F 'file=@file-path'，例如：`curl -F 'file=@/usr/bin/node' http://localhost:8080`
- curl -c cookie.txt url 访问 url 获得服务器给的 cookie 并存放到 cookie.txt 文件中
- curl -b cookie.txt url 访问 url 的同时，将 cookie 作为请求头发送给服务器
- curl -b cookie.txt -c cookie.txt url 同时发送 cookie，并接收服务器的 cookie

## 学习资料

- http://webres.wang/the-art-of-command-line/
- http://webres.wang/list-10-funny-linux-commands/
