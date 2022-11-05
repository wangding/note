# redis

## redis server 安装

docker 方式安装 mongodb。

```bash
touch docker-compose.yml
vi docker-compose.yml

version: '3.7'

services:
  redis:
    image: bitnami/redis:latest
    container_name: redis
    restart: always
    network_mode: "host"
    environment:
      - ALLOW_EMPTY_PASSWORD=yes

docker-compose up -d
docker ps -a
```

## 使用 docker 中的 redis-cli

不需要本地安装 redis-cli，直接使用 docker 中的 redis-cli。

```bash
docker run -it --rm --network host bitnami/redis:latest redis-cli
```

上面的命令太长，可以用 alias 定义别名。

```bash
alias redis='docker run -it --rm --network host bitnami/redis:latest redis-cli'
redis
```

## 验证 redis 是否正常工作

```bash
redis
help                              // 查看 redis 的帮助信息
keys *                            // 查看所有的键值对
set name wangding                 // 设置键
set mail wangding@heuet.edu.cn
keys *
get name          // 得到 name 键的值
get mail          // 得到 mail 键的值
exit              // 退出 MongoDB 系统
```

## redis 数据库编程操作

```bash
npm i -D mongodb
```

```javascript
#!/usr/bin/env node

const { MongoClient } = require('mongodb');

const log    = console.log,
      dbName = 'test',
      table  = 'log',
      dbURL  = 'mongodb://root:123@localhost:27017/?authMechanism=DEFAULT';

const client = new MongoClient(dbURL);

async function main() {
  await client.connect();
  log('Connected successfully to server');
  const db = client.db(dbName);
  const collection = db.collection(table);

  // modify data
  const arr = [2, 3];
  await collection.updateMany(
    { "logEvent": { $in: arr}},
    { $rename: {"createAt": "createAtt"}});

  return 'done.';
}

main()
  .then(console.log)
  .catch(console.error)
  .finally(() => client.close());
```
