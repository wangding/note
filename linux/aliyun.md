# 阿里云服务器操作

## 重新初始化系统盘

- 登录ECS管理控制台。
- 在左侧导航栏，单击实例与镜像 > 实例。
- 在顶部菜单栏左上角处，选择地域。
- 找到需要重新初始化系统盘的实例，单击实例 ID 进入实例详情页。
- 在左侧导航栏中，单击本实例云盘。
- 找到系统盘，在操作列中，单击重新初始化磁盘。
- 初始化操作的之前，要暂停实例，实例处于停止状态
- 在弹出的重新初始化云盘对话框里，配置重新初始化参数。
- 参数说明
- Linux实例：选择设置密钥或设置密码。
- 设置密钥：实例绑定 SSH 密钥对。后续通过 SSH 密钥方式登录。
- 设置密码：重新设置密码。可以使用旧的密码，也可以指定新的密码。
- 安全加固选择免费开通，您的实例会自动免费加载云服务器安全组件，提供网站后门检测、异地登录提醒、暴力破解拦截等安全功能。
- 启动实例策略选择重置云盘后启动，完成重新初始化后，实例会自动启动。
- 单击确认重新初始化云盘。

## 添加 wangding 用户

```bash
# 用 root 账号，执行下列操作

# 添加 wangding 用户
useradd wangding

# 把 wangding 加入到 root 组
gpasswd -a wangding root

# 查看 wangding 账户，所在的组
groups wangding

# 设置 wangding 账户的密码
passwd wangding

# 把 wangding 放到 sudoers 组
chmod 777 /etc/sudoers
vi /etc/sudoers

# wangding ALL ALL
chmod 440 /etc/sudoers
```

## 安装 nginx

```bash
# 安装依赖
sudo yum install -y pcre pcre-devel zlib zlib-devel openssl openssl-devel

# 下载 nginx 安装包
wget http://nginx.org/download/nginx-1.9.9.tar.gz

# 把压缩包解压
tar -zxvf  nginx-1.9.9.tar.gz

# 切换到 nginx 目录下
cd nginx-1.9.9

# 编译并安装
./configure
make
sudo make install

# 切换到 /usr/local/nginx 安装目录
cd /usr/local/nginx

# 编辑 nginx 的配置文件 nginx.conf 文件，默认不用编辑
vi conf/nginx.conf

# 启动 nginx
sudo sbin/nginx

# 检查 nginx 是否启动
ps -ef |grep nginx

# 用浏览器访问阿里服务器的公共 IP
# 应该能看到 nginx 的默认页面
```
