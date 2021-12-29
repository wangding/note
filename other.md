# 乱七八糟

## linux 进程间通信

六种方式方式，参考：https://blog.csdn.net/qq_34827674/article/details/107678226
- 管道
- 消息队列
- 共享内存
- 信号量
- 信号
- socket，参考：https://zhuanlan.zhihu.com/p/234806787

## pm2 线上环境
用 pm2 确保 linux 重启后，node.js 服务自动重启。

pm2 官网：https://pm2.keymetrics.io/
pm2 自动重启服务：https://pm2.keymetrics.io/docs/usage/startup/
主要是两个动作：
1. 用 pm2 startup 命令产生 systemd service 的配置文件；
2. 用 pm2 start app 启动服务程序；
3. 用 pm2 save 命令保存服务信息；
4. 重启 linux，用 pm2 ls 查看服务是否重启；

pm2 重启不成功的原因是使用了 nvm，导致执行 pm2 没有权限。
参考链接：PM2 + REHL8 for not root user: permission denied · Issue #4580 · Unitech/pm2 · GitHub

PM2 keeps getting killed every 90 seconds on centos 8,
解决办法：go to /etc/systemd/system/pm2-user.service - comment PIDFile=... (add a # in front of that line)

## sql 随机查询若干条记录

`select * from table order by rand() limit 100;`

## websocket 通过 https 
1. 客户端用 wss://domain-name:port/；
2. 服务器端用 https.createServer 添加证书；

## api 服务程序操作证书文件的权限
1. api 服务程序没有读取证书文件的权限，开始用 root 账户运行服务程序；
2. 检查后发现证书文件 u+r, g 和 o 没有 read 权限，chmod 添加了 read 权限后，user 账户下运行 app.js 没有报错了；
