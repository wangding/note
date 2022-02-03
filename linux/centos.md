# CentOS

## 命令行快捷键

- `ctrl + a` 移动光标到行首  ahead
- `ctrl + e` 移动光标到行尾  end
- 
- `ctrl + f` 按字符前移（右） forward
- `ctrl + b` 按字符后移（左） backward
- `alt  + f` 按单词前移（右） forward
- `alt  + b` 按单词后移（左） backward
- 
- `ctrl + w` 删除光标前面的一个单词
- `alt  + d` 删除光标后面的一个单词
- 
- `ctrl + k` 从光标处删除至命令行尾
- `ctrl + u` 从光标处删除至命令行首
- 
- `ctrl + r` 逆向搜索命令历史
- `ctrl + d` 删除当前字符
- `ctrl + h` 删除光标前一个字符
- 
- `ctrl + l` 窗口清屏，效果等同命令 clear
- 
- `alt  + c` 从光标处更改为首字符大写的单词 capital
- `alt  + u` 从光标处更改为全部大写的单词   upper
- `alt  + l` 从光标处更改为全部小写的单词   lower
- 
- `ctrl + t` 交换光标处和之前的字符
- `alt  + t` 交换光标处和之前的单词
- 
- `alt + .` 引用上一个命令的最后一个参数，等价于 `!$`

在 xshell 中使用 alt 快捷键，需要进行设置，否则会和 window 窗口的快捷键冲突：

## 常用命令

- `&`：在后台执行
- `&&`：逻辑与
- `*`：匹配任意长度的任意字符
- `?`：匹配任意一个字符
- `[]`：匹配属于字符组的字符
- `|`：管道符，用于连接多个命令，前一个命令的输出作为后一命令的输入
- `||`：逻辑或
- `<`：输入重定向
- `>`：输出重定向
- `>>`：附加到指定文件的结尾
- `awk`：过滤器
- `basename`：提取基本文件名
- `cal`：显示日历
- `cat`：一次性显示输出文件的全部内容
- `cd`：改变当前工作目录
- `chgrp`：修改文件或目录的用户组
- `chmod`：修改文件或目录的权限
- `chown`：修改文件或目录的所有者
- `clear`：清屏，提示符回到屏幕左上方
- `cp`：复制文件
- `cut`：剪切文件
- `date`：显示当前日期和时间
- `df`：对文件系统的磁盘空间使用情况进行统计
- `diff`：比较两个文件的差异
- `echo`：回显，即将字符串输出到标准输出设备
- `egrep`：支持正则表达式的 grep 命令
- `file`：显示文件的类型
- `find`：查找指定的文件
- `grep`：查找指定的字符串
- `head`：查看文件的开始部分，默认为前 10 行
- `ls`：列出目录中的内容
- `man`：显示联机参考手册
- `mkdir`：创建目录
- `more`：分屏显示文件的内容
- `mv`：移动文件
- `netstat`：显示网络状态
- `passwd`：修改用户密码
- `ps`：显示进程相关信息
- `pwd`：显示当前目录
- `rm`：删除文件
- `rmdir`：删除目录，要求目录非空
- `sed`：流编辑器
- `sleep`：暂停指定的时间间隔
- `su`：临时切换到另一用户
- `tail`：查看文件的结尾部分，默认为后 10 行
- `Talk`：与其他用户对话
- `vi`：vim 编辑器
- `wc`：计算文件的单词数、行数、字符数
- `who`：显示当前登录的用户的信息
- `write`：给指定用户发消息
- `shutdown -r now`，重启 linux 系统
- `shutdown -h now`，关闭 linux 系统
- `ls -R`，显示所有子目录和文件
- `cat /etc/redhat-release`，查看 centOS 版本
- `rpm -aq`，查看本机安装的软件包
- `ps -ef`，查看系统中的进程
- `which firewalld`，查看进程 firewalld 用到的命令
- `kill pid`，杀掉 pid 的进程
- `kill -9 970`，强制删除 970 进程
- `gsettings set org.gnome.desktop.interface cursor-blink false`，设置终端光标不闪烁
- `passwd wangding`，修改当前用户 wangding 账户的密码
- `sudo hostnamectl --static set-hostname DEV`，设置主机名为 DEV
- `hostnamectl status`，查看主机名信息
- `$(cmd)`，把 cmd 的运行结果放到其他命令中，例如：`echo "今天是：$(date)"`
- `xxd hello.o`，在控制台查看二进制文件

## 使用 man 命令查看系统调用

man 2 read 或者是 man 3 read。中间的数字是什么意思呢？是man的分卷号，原来man分成很多部分，分别是：

- 1 用户命令，可由任何人启动的
- 2 系统调用，即由内核提供的函数
- 3 例程，即库函数，比如标准 C 库 libc
- 4 设备，即 /dev 目录下的特殊文件
- 5 文件格式描述，例如：/etc/passwd
- 6 游戏
- 7 杂项，例如宏命令包、惯例等
- 8 系统管理员工具，只能由 root 启动
- 9 其他（Linux 特定的），用来存放内核例行程序的文档
- n 新文档，可能要移到更适合的领域
- o 老文档，可能会在一段期限内保留
- l 本地文档，与本特定系统有关的

要查属于哪一部分的，就用哪一部分的编号在命令之前。

一般系统没有 man 命令，如果只安装 man，就只能查看第一部分（命令），如：

`yum install man -y`

如果要查看函数，也就是后面的部分，还需要安装 man-pages

`yum install man-pages -y`
`yum install man-pages-zh-CN -y`

## CentOS 查看系统版本

- `uname -a`
- `cat /etc/redhat-release`

## diff

比较文件之间的差异。
```bash
# -y 参数平铺文档
# -b 忽略空格差异
# -B 忽略空行差异
diff a.c b.c -y -b -B
```
比较结果的符号说明：
- “|”表示前后2个文件内容有不同  
- “<”表示后面文件比前面文件少了1行内容  
- “>”表示后面文件比前面文件多了1行内容  

## linux bash 邮件客户端

```
yum -y install sendmail
yum -y install mailx

sudo yum -y install mailx sendmail

mail -s 'test' 408532507@qq.com < a.txt
```

## 查看进程树

pstree 查看进程树
yum install psmisc -y（安装 pstree）

ps -ef （可以看到 ppid）
ps -ajx （可以查看进程组号）

## scp 命令

```bash
# 复制文件到远程主机
scp /path/file root@ipaddr:/path/
# 例如：
scp index.js wangding@192.168.59.148:/home/wangding/wd/auto/

# 从远程主机复制文件到本地
scp root@ipaddr:/path/file .
# 例如：
scp wangding@192.168.59.144:/home/wangding/wd/auto/index.js .
```

## 安装卸载程序

- `yum list installed`，列出已经安装的软件包
- `yum list`，列出已安装的和可安装的应用程序包
- `yum list package`，列出 package 应用的安装情况
- `yum clean`，清除缓存的软件包信息
- `/etc/yum.repos.d/\*.repo`，yum 源定义文件
- `yum install package`，安装 package
- `yum remove package`，删除 package
- `yum update package`，升级 package
- `yum list updates`，列出所有可以升级的软件包

## 启动服务

- `systemctl start mariadb`，启动 mariadb 数据库服务
- `systemctl start httpd`，启动 apache 服务
- `systemctl status httpd`，查询 apache 服务是否启动
- `systemctl restart httpd`，重新启动 apache 服务
- apache 服务启动不正常的解决办法，`firewall-cmd --add-service=http`

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

## 用户、组和文件权限

- `useradd wangding`，添加新用户 wangding
- `vipw`，命令查看系统中的用户，一般新添加的用户都在文件的最后一行
  查看的信息包括：用户 ID 和主 ID，用户家目录，用户的 shell
- `groupadd abc`，添加 abc 用户组
- `vigr`，命令查看用户组的信息，vipw 命令和 vigr 命令是有规律的，vi 代表 vi 编辑器，其实是用 vi 编辑器查看信息的。pw 代表 password 用户，gr 代表 group 用户组。查看的信息包括：组的 ID 和组的成员。
- `gpasswd -a username groupname`，把用户加到组中
- `groups wangding`，查看用户 wangding 所在的用户组信息
- `whoami`，查看当前登录的用户
- `su` - 切换到 root 用户，su 是 switch user 的缩写
- `su - wangding`，将当前用户环境切换到 wangding 用户环境下面，退出用 exit
- `userdel wangding`，删除用户 wangding
- `groupdel`，删除组
- `id root`，查看 root 用户的 ID 值，ID 值越小权限越大
- `chmod permission filename`，修改文件权限
- `permission：r=4, w=2, x=1, rw=4+2=6, rx=4+1=5`, 等等，用户权限，组权限和其他用户权限，按顺序依次为三个组
- `chown user filename`，改变文件或目录的所有者，ch: change, own：owner
- `chgrp group filename`，改变文件或目录的组名
- `chown user.group filename`，改变文件或目录的所有者为 group 组的 user 用户

## 常用网络命令

- ssh，远程登录或执行远程主机上的命令，参考链接：https://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html
- hostname
- ping
- ifconfig
- iwconfig
- nslookup
- telnet
- netstat
- nc，net cat，参考链接：http://www.linuxso.com/command/nc.html
- lsof，list open file，参考链接：https://www.jianshu.com/p/a3aa6b01b2e1

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
- `curl -F`，参数可以上传文件，参数格式：-F 'file=@file-path'，例如：`curl -F 'file=@/usr/bin/node' http://localhost:8080`
- `curl -c cookie.txt url`，访问 url 获得服务器给的 cookie 并存放到 cookie.txt 文件中
- `curl -b cookie.txt url`，访问 url 的同时，将 cookie 作为请求头发送给服务器
- `curl -b cookie.txt -c cookie.txt url`，同时发送 cookie，并接收服务器的 cookie

## ZSH 的 z 命令

- z 命令可以快速完成目录切换
- `z`，列出所有最近访问过的路径及权重，权重越大，越优先匹配
- `z -l [keyword]`，列出匹配 keyword 的路径及权重，keyword 可以是一个字母
- `z -t [keyword]`，跳转到最近使用的 keyword 路径，即使 keyword 权重较低
- zsh 的用法，[为什么说 zsh 是 shell 中的极品？](https://www.zhihu.com/question/21418449/answer/91817026)

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

## 网络设置

```bash
vi /etc/sysconfig/network-scripts/ifcfg-ens32

# 地址是否自动获得 none 不自动获得，否则 dhcp 为自动获得
BOOTPROTO=dhcp

# 是否自动加载
ONBOOT=yes
```

## 启用 OpenSSH

参考：http://wangsheng1.blog.51cto.com/29473/1548853/

## 常见问题

- 用户 sudo 不在 sudoers 用户组中的问题
http://blog.csdn.net/attagain/article/details/11987297

## 字体美化

- http://www.jinbuguo.com/gui/fonts.conf.html

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


## 通过 xshell windows 给 linux 虚拟机上传文件

http://www.linuxidc.com/Linux/2015-05/117975.htm

## linux 查找文件内容

```bash
grep "hello" ./*.js  # 在当前目录的所有 js 文件中查找 hello 字符串
```

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

## 参考资料

- [快乐的 Linux 命令行](http://billie66.github.io/TLCL/book/index.html)
- [Bash 快捷键大全](https://linux.cn/article-5660-1.html)
- http://webres.wang/the-art-of-command-line/
- http://webres.wang/list-10-funny-linux-commands/
- 操作系统：https://github.com/sunym1993/flash-linux0.11-talk
- linux 性能分析：https://zhuanlan.zhihu.com/p/35879028
- 笨办法学 linux 视频：https://v.qq.com/biu/videoplus?vuid=327037319
- LFS 中文：https://lctt.github.io/LFS-BOOK/lfs-sysv/LFS-BOOK.html
