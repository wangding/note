【参考资料】  

- JSDoc 文档资料: http://www.css88.com/doc/jsdoc/index.html  
- JSDoc 工具下载: https://www.npmjs.com/package/jsdoc
- JSDoc 的 vim 插件的内容，参考：vim.md  
- JavaScript 编码规范：https://standardjs.com/readme-zhcn.html

# JavaScript 忍者秘籍

## 第 7 章 正则表达式

## 7.1 为什么正则表达式很牛

因为正则表达式可以节省代码。

正则表达式的网站：http://www.regexplanet.com/advanced/javascript/index.html

## 7.2 正则表达式进阶

### 7.2.1 正则表达式解释

```javascript
var pattern = /test/;                   // 正则表达式字面量
var pattern = new RegExp('test');       // 动态构建正则表达式
var pattern = new RegExp('test', 'ig')  // 第二个参数，正则表达式标志
```

三个表达式标志：

- i 不区分大小写，/test/i
- g 全局匹配，只是默认只匹配第一次出现的结果，/test/g
- m 匹配多行，/test/m

### 7.2.2 术语与操作符

- 精确匹配，例如：/test/
- 匹配一类字符，例如：/[abcd]/，/[^abc]/，/[a-d]/
- 转义特殊字符如：`^、$、[`，另外见下面的预定义字符，例如：/\[/，/\n/
- 匹配开始 `^` 与匹配结束 `$`，例如：/^test/，/test$/，/^test$/
- 重复出现：
  - ? 可选，出现一次或者不出现，例如：/t?est/  
  - + 出现一次或者多次，例如：/t+est/
  - * 出现零次或者多次，例如：`/t*est/`
  - {n}，{n,m}，{n,}，{,m}，例如：/t{2,4}est/
- 预定义字符
  - \r 回车
  - \n 换行
  - \s 匹配空白字符，包括：空格、制表符、换页符，等
  - \d 匹配任意数字，等价：[0-9]
  - \D 匹配任意非数字，等价：[^0-9]
  - \w 匹配包括下划线的任意单词字符，等价于 `[A-Za-z0-9_]`
  - \W 匹配任何非单词字符，等价于 `[^A-Za-z0-9_]`
  - .  匹配除了换行 \n 之外的任意字符
  - \b 空格
  - \v 垂直制表符
  - \f 换页符
  - \t 水平制表符
- 分组，例如：/(ab)+/
- 或操作符，例如：/(ab)+|(cd)+/
- 反向引用，\1，\2 一般和分组结合使用，例如：`/<(\w+)>(.+)<\/\1>/`

## 7.3 编译正则表达式

正则表达式的两个重要阶段是：
- 编译，正则表达式第一次被创建时
- 执行，编译过的正则表达式进行字符串匹配时

正则表达式可以是编程时指定，也就是正则表达式字面量。
也可以在运行时指定，就是用字符串作为参数，调用 `new RegExp()` 创建正则表达式。注意，正则表达式字面量 \s 在字符串中应该表示为 '\\s'，其中 `\\` 表示斜杠的转义。

## 7.4 捕获匹配的片段

### 7.4.1 执行简单的捕获

```javascript
var str = 'ac--bc'
str.match(/[ab]c/)
```
返回第一个匹配的结果

### 7.4.2 用全局表达式进行匹配

```javascript
var str = 'ac--bc'
str.match(/[ab]c/g)
```
返回所有匹配的结果

```javascript
var html = '<div class="test"><b>hello</b><i>world!</i></div>'
html.match(/<(\/?)(\w+)([^>]*?)>/)
html.match(/<(\/?)(\w+)([^>]*?)>/g)
```

注意观察两个 match 的结果，这是两个不同的数组。match 的行为主要受到 /g 的影响。没有 /g 全局匹配的时候，match 只匹配第一个，如果没有匹配则返回 null。如果匹配成功，则返回一个数组，数组的第一个元素是整个匹配项，数组的其他匹配项，则是正则表达式的匹配子项。

```javascript
var html = '<div class="test"><b>hello</b><i>world!</i></div>'
var reg = /<(\/?)(\w+)([^>]*?)>/g
reg.exec(html)
reg.exec(html)
```
反复调用 exec 方法，该方法保存了上一次调用的状态。

### 7.4.3 捕获的引用

```javascript
"ninja-ninja-sword".match(/((ninja-)+)sword/)
"ninja-ninja-sword".match(/((?:ninja-)+)sword/)
```
在括号后加上 ?: 标记，这就是所谓的被动子表达式，该表达式只会为外层的括号创建捕获。

## 7.5 利用函数进行替换

```javascript
function upper(letter) { return letter.toUpperCase();  }
'border-bottom-width'.replace(/-(\w)/g, upper)
```

```javascript
function compress(source) {
  var keys ={};
  source.replace(/([^=&]+)=([^&]*)/g, function(full, key, value) {
    //console.log('full = %s, key = %s, value = %s', full, key, value);
    //console.log('before: ', keys);
    keys[key] = (keys[key] ? keys[key] + ',' : '') + value;
    //console.log('after: ', keys);
    return '';
  });
  console.log('keys: ', keys);

  var result = [];
  for(var key in keys) {
    result.push(key + '=' + keys[key]);
  }
  return result.join('&');
}

var str = 'foo=1&foo=2&blash=a&blash=b&foo=3';
//console.log('str = %s', str);
console.log(compress(str));
```


【补充】  
- 测验和练习，可以在 chrome 控制台中执行下面的代码：

测试正则表达式的模式：
```javascript
var reg = /test/
reg.test('testt')
```

捕获字符串模式：
```javascript
var str = 'ac--bc'
str.match(/[ab]c/)
str.match(/[ab]c/g)
```


# JavaScript 语言精解

## JavaScript 基础：值、变量、控制流程

1.1 值

六种基本类型：number、string、boolean、object、function 和 undefined

1.1.1 数字

1.1.2 算术

+、-、\*、/、%

1.1.3 字符串

+ 连接字符串
\ 转义字符

1.1.4 一元运算符

typeof、!

1.1.5 布尔值、比较和布尔逻辑

>、<、>=、<=、==、!=
&&、||

1.1.6 表达式与语句

1.2 变量

关键字与保留字

1.3 环境

1.3.1 函数

1.3.2 prompt 和 confirm

1.3.3 print 函数

1.3.4 修改环境

1.4 程序结构

1.4.1 条件执行

1.4.2 while 循环与 do 循环

1.4.3 缩进代码

1.4.4 for 循环

1.4.5 跳出循环

break

1.4.6 更新变量简便法

+=、-=、++、--

1.4.7 使用 switch 进行调度




## 文字教程学习资料

- 阮一峰的 JavaScript 教程  
  http://javascript.ruanyifeng.com/  
- 廖雪峰的 JavaScript 教程  
  http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000  
- 独孤求败的全栈教程：  
  https://happypeter.github.io/digicity/

## 视频课程学习资料

- 李炎恢老师的视频课程  
  http://edu.51cto.com/course/course_id-166.html

## 在线通关练习资料

- Node 大学的资料
  - javascripting
  - scope-chains-closures
  -
