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

## bitnami redmine

- https://docs.bitnami.com/virtual-machine/faq/#how-to-remotely-access-the-bitnami-application
- https://docs.bitnami.com/virtual-machine/faq/#how-to-connect-to-the-server-through-ssh

## 研究 redmine 插件

## redmine Mysql

mysql -u root -p 虚拟机上的密码

