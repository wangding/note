# mariadb

## 安装 MariaDB

```bash
su
yum install -y mariadb mariadb-server
systemctl start mariadb
```

## 配置 MariaDB

```bash
mysql_secure_installation
```

## 访问 MariaDB

```bash
su
mysql -p
```

-p 参数会提示输入密码，输入密码后，就可以访问数据库了。
