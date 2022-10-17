# mongoDB

## mongodb server 安装

docker 方式安装 mongodb。

```bash
touch docker-compose.yml
vi docker-compose.yml

version: '3.7'

services:
  mongodb-primary:
    container_name: mongodb
    image: 'bitnami/mongodb:latest'
    restart: always
    network_mode: "host"
    environment:
      - MONGODB_ROOT_PASSWORD=123

docker-compose up -d
docker ps -a
```

## 使用 docker 中的 mongosh

不需要本地安装 mogodbsh，直接使用 docker 中的 mongosh。

```bash
docker run -it --rm --network host bitnami/mongodb:latest mongosh
```

上面的命令太长，可以用 alias 定义别名。

```bash
alias mg='docker run -it --rm --network host bitnami/mongodb:latest mongosh'
mg -u root -p
```

## 本地安装 mongosh

```bash
sudo touch  /etc/yum.repos.d/mongodb.repo
sudo vi /etc/yum.repos.d/mongodb.repo

[mongodb-org-6.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/6.0/$basearch/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-6.0.asc

sudo yum install mongodb-mongosh -y
mongosh --version
```

## 验证 mongodb 是否正常工作

```bash
mongosh -u root -p 123
help           // 查看 MongoDB 的帮助信息
db.help()      // 查看数据库的帮助信息
db.version()   // 查看 MongoDB 的版本号
show dbs       // 查看有多少个数据库
use todo       // 使用 todo 库作为当前的数据库
db             // 查看当前的数据库
exit           // 退出 MongoDB 系统
```

## DDL

```javascript
use demo                      // 建库，如果 demo 库不存在会创建
db.createCollection('areas')  // 创建 areas 表
show collections
db.areas.drop()               // 删除集合
db.dropDatabase()             // 删除当前的数据库
```

## DML

```javascript
// 向 areas 表插入一条记录
db.areas.insert({'area_name': '日韩'})
db.areas.insert({'area_name': '欧美'})

// 查看 areas 表的所有记录
db.areas.find()

// 查看 areas 表中的特定记录
db.areas.find({'area_name': '日韩'})

// 查看 areas 表中的记录数量
db.areas.countDocuments()

// 对 areas 表排序，trade_date 是表中需要排序的字段，相当于 order by trade_date
// 1 代表升序，-1 代表降序
db.areas.find().sort({ 'trade_date': 1})
db.areas.find().sort({ 'trade_date': 1}).limit(10)      // 查看前 10 条数据
db.areas.find({}, {trade_date: 1, open: 1, close: 1})   // 只查看表中的三个字段
db.areas.findOne();    // 返回符合查询条件的第一条记录

// 删除 areas 表中符合条件的记录
db.areas.deleteMany({})

// 将旧文档换成新文档
db.areas.update(old, new)
```

## DCL

略

## 执行脚本

```bash
mongosh -u root -p -f a.js
```

## mongodb 数据库编程操作

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
