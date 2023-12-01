# SQLite

## 参考资料

- [SQLite 官网](https://www.sqlite.org/)
- [SQLite 中文文档](https://sqlite.readdevdocs.com/docs.html)
- [SQLite3 快速入门](https://www.bilibili.com/video/BV1ua4y1Z7AZ/)

## 安装 SQLite3

- CentOS 7

```bash
yum install sqlite-devel
```

- Ubuntu

```bash
sudo apt update
sudo apt install sqlite3
```

## SQLite3 的基本操作

```bash
touch app.db      // 创建空数据库文件 app.db
sqlite3 app.db    // sqlite3 打开数据库文件，后续操作会反映到数据库文件中
                  // 不跟数据库文件，后续操作都在内存数据库中，退出后会丢失成果
>.read setup.sql  // 执行建库建表脚本 setup.sql
>.tables          // 查看有哪些表
>.mode column     // 设置查看方式，表格查看
>select * from users; // 查询数据库
>.quit
```

## nodejs 操作SQLite3 数据库

- 使用 [better-sqlite3](https://www.npmjs.com/package/better-sqlite3) 模块
- better-sqlite3 的方法都是**同步**的

```javascript
const Database = require('better-sqlite3');
const { join } = require('path');
const dbFile = join(__dirname, 'app.db');
const db = new Database(dbFile) // 这里一定要使用绝对路径
                                // 相对路径会碰到表找不到的错误
// insert
db.prepare('insert into users(login_name) values(?)')
  .run('lisi');

// update
db.prepare('update users set login_name = ? where id = ?')
  .run('zhangsan', 1);

// delete
db.prepare('delete from users where id = ?')
  .run(2);

// select
const rows = db.prepare('select * from users where id = ?')
               .all(1);

console.table(rows)
db.close;
```

## northwind 数据库

- 下载 [northwind-sqlite.sql](./northwind-sqlite.sql)
- 运行该脚本建库建表
- 在 northwind 数据库中练习 SQL 编程
