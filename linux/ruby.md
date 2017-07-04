# 安装 ruby

用 ruby-install 来安装 ruby。用 root 用户登录 linux，假设 linux 是 CentOS 最小系统。

## 安装必要工具

```bash
yum install -y wget bzip2
```

## 安装 ruby-install

```bash
wget -O ruby-install-0.6.1.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.1.tar.gz
tar -xzvf ruby-install-0.6.1.tar.gz
cd ruby-install-0.6.1/
make install
```

## 安装 ruby

安装最新的 ruby 稳定版

```bash
ruby-insatll --system ruby
ruby -v
```
