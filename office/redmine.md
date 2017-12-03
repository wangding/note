# redmine 项目管理

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

