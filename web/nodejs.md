# Node.js

## node.js 应用上线

一、pm2 线上环境
用 pm2 确保 linux 重启后，node.js 服务自动重启。

- [pm2 官网](https://pm2.keymetrics.io/)
- [pm2 自动重启服务](https://pm2.keymetrics.io/docs/usage/startup/)

主要是两个动作：
1. 用 pm2 startup 命令产生 systemd service 的配置文件；
2. 用 pm2 start app 启动服务程序；
3. 用 pm2 save 命令保存服务信息；
4. 重启 linux，用 pm2 ls 查看服务是否重启；

pm2 重启不成功的可能原因是用了 nvm，导致执行 pm2 没有权限。
参考链接：https://github.com/Unitech/pm2/issues/4580

PM2 keeps getting killed every 90 seconds on centos 8,
解决办法：go to /etc/systemd/system/pm2-user.service - comment PIDFile=... (add a # in front of that line)

## Puppeteer google 出的无头浏览器

- 文章 1：https://www.jianshu.com/p/2f04f9d665ce
- 文章 2：https://www.jb51.net/article/138391.htm
- 官网：https://github.com/GoogleChrome/puppeteer
- API：https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md
- 应用：Node.js 前端技术，爬虫或者 UI 自动化测试

## nvm Node.js 版本管理

nvm Node.js Version Manager

Node.js 版本管理有两个工具：nvm 和 n，这两个工具的比对，请看文章：http://taobaofed.org/blog/2015/11/17/nvm-or-n/

如果想在同一台机器，同时安装多个版本的 Node.js，就需要用到版本管理工具 nvm。

用下面的方式安装 nvm。

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

安装以后，nvm 的执行脚本，每次使用前都要激活，建议将其加入 ~/.bashrc文件（假定使用Bash）。激活后，就可以安装指定版本的 Node。

```bash
# 安装最新版本
$ nvm install node

# 安装指定版本
$ nvm install 6

# 使用已安装的最新版本
$ nvm use node

# 使用指定版本的node
$ nvm use 0.12
```

nvm 也允许进入指定版本的 REPL 环境。

```bash
$ nvm run 0.12
```

如果在项目根目录下新建一个 .nvmrc 文件，将版本号写入其中，就只输入 nvm use 命令即可，不再需要附加版本号。

下面是其他经常用到的命令。

```bash
# 查看本地安装的所有版本
$ nvm ls

# 查看服务器上所有可供安装的版本。
$ nvm ls-remote

# 退出已经激活的nvm，使用deactivate命令。
$ nvm deactivate
```

## pm2 进程管理

pm2 工具非常强大，是一个生产环境下 Node.js 进程管理工具：

- GitHub 仓库：https://github.com/Unitech/pm2
- 可以查看程序的输出日志 `pm2 logs`, `pm2 monit` 
- 可以监视代码文件的变更 `pm2 start app --watch`
- 代码文件变更之后，会重新启动服务程序
- 可以在 app 后面增加参数 `pm2 start app -- app-argument`

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
## 其他

一、sql 随机查询若干条记录

select * from table order by rand() limit 100;

二、web socket 通过 https
1. 客户端用 wss://domain-name:port/；
2. 服务器端用 https.createServer 添加证书；

三、api 服务程序操作证书文件的权限
1. api 服务程序没有读取证书文件的权限，开始用 root 账户运行服务程序；
2. 检查后发现证书文件 u+r, g 和 o 没有 read 权限，chmod 添加了 read 权限后，user 账户下运行 app.js 没有报错了；

## 文字教程

- 教程：https://www.nodejs.red/
- Node.js 包教不包会：https://github.com/alsotang/node-lessons
- 七天学会 NodeJS：https://github.com/nqdeng/7-days-nodejs
- Node.js 入门：https://cnodejs.org/getstart
- 张丹的 nodejs 博客：http://blog.fens.me/series-nodejs/
- node 大学在线教程：https://nodeschool.io/zh-cn/
- 阮一峰的 JavaScript 教程中有 NodeJS 的内容：http://javascript.ruanyifeng.com/nodejs/basic.html
- 极客学院的 wiki 有 nodejs api 中文：http://wiki.jikexueyuan.com/project/nodejs/
- 饿了吗 Node.js 面试题：https://github.com/ElemeFE/node-interview/blob/master/sections/zh-cn/README.md
- Node.js 中文社区：https://cnodejs.org/
- 程序猿小卡的 Node.js 学习笔记：https://github.com/chyingp/nodejs-learning-guide
- 一起学 Node.js（有一个完整的大案例）：https://github.com/nswbmw/N-blog
