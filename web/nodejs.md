# Node.js

## 刘士的 gitbook 插件

- 他的个人主页：https://liushilive.github.io/
- 他的软件测试必知必会内容很丰富
- 他的 gitbook 插件挺好用：https://github.com/liushilive/books-cli
- 我的电子书都用上他的插件了

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

## 文字教程

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

## 视频教程

- 慕课网 scott 的 NodeJS 进阶  
- 51CTO 学院何韬的 NodeJS 视频  
- 51CTO 学院曾亮的 Nodejs 视频
- 51CTO 学院李宁的 NodeJS 视频 
- [Node.js Tutorials for Beginners](https://www.youtube.com/playlist?list=PL6gx4Cwl9DGBMdkKFn3HasZnnAqVjzHn_)

