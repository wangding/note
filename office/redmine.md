# Redmine 项目管理

## 安装 Redmine

### 安装 ruby

- CentOS 7 安装 ruby 2.6
- 安装步骤如下

```bash
# 查看系统当前 ruby 版本
ruby -v

# 通过 yum 安装 ruby 和依赖的包
sudo yum -y install ruby ruby-devel rubygems rpm-build

# 查看 ruby 版本，应该是 2.0 版本，版本较低
ruby -v

# 安装 ruby 依赖
sudo yum -y install gcc-c++ patch readline readline-devel \
zlib zlib-devel libyaml-devel libffi-devel openssl-devel \
make bzip2 autoconf automake libtool bison iconv-devel \
sqlite-devel wget mysql-devel

# 修改 ruby 的 gem 源

# 查看查看当前使用的源地址
gem sources

# 添加国内镜像地址
gem sources -a https://gems.ruby-china.com/

# 删除默认的源地址
gem sources -r https://rubygems.org/

# 更新源的缓存
gem sources -u

# 安装 rvm

# 获取密钥
gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

# 安装 rvm
curl https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer | bash -s stable

# 更新配置文件
source /home/wangding/.rvm/scripts/rvm

# 查看所有可安装版本
rvm list known

# 修改 rvm 源
echo "ruby_url=https://cache.ruby-china.com/pub/ruby" > ~/.rvm/user/db

# 安装 ruby 2.6
rvm install 2.6

# 更改 gem 国内源
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
gem sources -l
# 确保只有 gems.ruby-china.com

# 安装 rails
gem install rails

# 检查 rails 的版本
rails -v

# 检查 ruby 的版本
ruby -v

# 检查 gem 的版本
gem -v
```

### 下载 redmine 原代码

- `wget --no-check-certificate https://redmine.org/releases/redmine-4.1.1.tar.gz`
- 解压缩，`tar zxvf redmine-4.1.1.tar.gz`

### 创建 redmine 数据库

- 用下面的 SQL 脚本创建 redmine 数据库

```sql
CREATE DATABASE redmine CHARACTER SET utf8mb4;
CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'my_password';
GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
```

### 编辑数据库连接的配置文件

- 进入 redmine 代码文件夹，`cd redmine-4.1.1/`
- 复制代码文件，`cp config/database.yml.example config/database.yml`
- 编辑 `database.yml`

### 安装 redmine 项目依赖

- 安装 bundler, `gem install bundler`
- 配置 bundler 国内源，`bundle config mirror.https://rubygems.org https://gems.ruby-china.com`
- `gem install mysql2 -v '0.5.3'`
- 安装项目依赖，`bundle install --without development test`

### 创建 Session 加密 token

- `bundle exec rake generate_secret_token`

### 创建数据库的表结构

- `RAILS_ENV=production bundle exec rake db:migrate`

### 初始化 redmine 数据库数据

- `RAILS_ENV=production bundle exec rake redmine:load_default_data`

### 启动 redmine 服务

- `bundle exec rails server webrick -e production`

### 登录 redmine

- 用户名：admin
- 密码：admin

## 配置 redmine 邮件服务

- 进入 redmine 代码目录，`cd redmine-4.1.1`
- 修改默认配置文件名，`mv config/configuration.yml.example config/configuration.yml`
- 编辑配置文件，`vi config/configuration.yuml`
- 使用 163 邮箱的配置信息如下，其他邮箱类似：

```yml
production:
  email_delivery:
    delivery_method: :smtp
    smtp_settings:
      ssl: true
      address: "smtp.163.com"
      port: 465
      domain: '163.com'
      authentication: :login
      user_name: 'email address'
      password: '授权码'
```

## ssh 连接 bitnami redmine vm

```bash
sudo rm -f /etc/ssh/sshd_not_to_be_run
sudo systemctl enable ssh
sudo systemctl start ssh
```

用 xshell 连接 bitnami redmine vm

## Git 版本库配置

- http://www.redmine.org/projects/redmine/wiki/HowTo_Easily_integrate_a_(SSH_secured)_GIT_repository_into_redmine
- http://www.redmine.org/projects/redmine/wiki/RedmineRepositories#Git-repository
- http://www.redmine.org/projects/redmine/wiki/HowTo_configure_Redmine_for_advanced_git_integration

分以下三个步骤：

1. 在 bitnami redmine 服务器上创建远程仓库的镜像仓库

注意，不能用 --bare 参数，因为 bare 只能作为服务器，接受 push，不能从远程仓库 fetch 拉取合并更新。
【参考资料】：http://blog.sina.com.cn/s/blog_72ef7bea0101gcao.html

```bash
cd
mkdir repos
cd repos
git clone --mirror https://github.com/wangding/git-demo
```

2. 配置 Redmine 的 Git 参数

Redmine 上设置 Git 参数

- SCM：Git
- 主版本库：true
- 标识：git-demo (跟仓库的名字相同)
- 库路径：/home/bitnami/repos/git-demo.git

3. 在服务器上编写 crontab 计划任务

定时拉取远程仓库。

```bash
cd /home/bitnami/repos/git-demo.git && sudo git fetch --all
```

## bitnami redmine

- https://docs.bitnami.com/virtual-machine/faq/#how-to-remotely-access-the-bitnami-application
- https://docs.bitnami.com/virtual-machine/faq/#how-to-connect-to-the-server-through-ssh

## 研究 redmine 插件

## redmine Mysql

mysql -u root -p 虚拟机上的密码


