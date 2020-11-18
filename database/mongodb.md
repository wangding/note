# mongoDB

基本概念：库，集合（表），文档（记录）

## mongo shell

```bash
# 进入 shell
mongo

# 显示所有数据库
show dbs

# 使用 todo 库作为当前的数据库
use todo

# 查看当前的数据库
db

# 显示该库下的所有表
show collections

# 退出 mogo shell
exit
```

## DDL

```javascript
// 建库，如果 abc 库不存在，use abc 会创建 abc 数据库
use abc

// 创建 abc 表
db.createCollection('abc')
```

## DML

```javascript
// 向 abc 表插入一条记录
db.abc.insert({'name': 'wangding', 'pwd': '123'})
db.abc.insert({'name': 'lisi', 'pwd': 'abc'})

// 查看 abc 表的所有记录
db.abc.find()

// 查看 abc 表中的特定记录
db.abc.find({'name': 'wangding'})

// 查看 abc 表中的记录数量
db.abc.count()

// 对 abc 表排序，trade_date 是表中需要排序的字段，相当于 order by trade_date
// 1 代表升序，-1 代表降序
db.abc.find().sort({ 'trade_date': 1})
db.abc.find().sort({ 'trade_date': 1}).limit(10)          // 查看前 10 条数据
db.nyyh.find( {}, { trade_date: 1, open: 1, close: 1 } )  // 只查看表中的三个字段，第一个花括号是查询条件，没有查询条件

// 删除 abc 表中的所有记录
db.abc.remove({})
```

## DCL

(略)
