# 相关资源

- 正则表达式在线开发和测试工具：https://regex101.com/

# JavaScript 中的正则表达式

参考资料：《JavaScript 忍者秘籍》第 7 章 正则表达式

以下是学习笔记。

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
  - 贪婪和非贪婪，默认是贪婪的，可以用 ？改变，例如：/t+?est/
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
- 正向先行断言，(?=) 括号里面的代表位置，不做匹配

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

# Linux 中的正则表达式

正则表达式的语法基本相同。只不过 Linux Bash 中的正则表达式语法分为：基本的正则表达式和扩展的正则表达式，两个加起来就是 JavaScript 的正则表达式。

## grep 命令实现文本搜索

grep 命令的格式如下：

grep [options] regex [file...]

options：
-i 忽略大小写
-E 使用扩展的正则表达式语法

另外，对于命令行有特别用途的元字符，例如：`*`，如果出现在正则表达式中，需要用 `\` 转义。

例如：
在 `~/wd/nodejs-demo/` 目录下面找所有 `.js` 扩展名的文件，执行如下命令：

```bash
find . | grep ".js"                        // 会匹配 .json 文件
find . | grep ".js$"                       // 会匹配 node_module 目录下的 *.js 文件
find . | grep "^\.\/.*js$"                 // 会匹配 node_module 目录下的 *.js 文件
find . | grep "^\.\/[0-9]\{2\}.*js$"       // 正确匹配，匹配上的文字呈现红色
```

注意 PATTERN 被双引号引用起来以防止被 Shell 解析。

- Linux 基础命令介绍五：文本过滤 grep：https://segmentfault.com/a/1190000007416745

## less 中用正则表达式搜索

/后面是正则表达式

## vim 中的正则表达式

vim 支持基本的正则表达式，只是正则表达式的写法略微有些区别。我们看到表达式几乎一样；然而，在扩展表达式中，许多被认为是元字符的字符在基本的表达式中被看作是文本字符。只有用反斜杠把它们转义之后，它们才被看作是元字符。

/后面是正则表达式，实现文本搜索

:%s/正则表达式/新文本/g，实现全局正则表达式搜索替换。注意，最好在替换之前先搜索一下，相当于对正则表达式做一下测试，以免正则表达式错误导致文本的意外更改。
s 是 substitute 替换的意思，前面的 % 相当于 1,$ 代表替换范围是整个文档。其中正则表达式中斜杠如果太多 / 可以用其他符号替代，比如：?。

例如：`:s?^\(\s*\)\(.*\)\s*$? \1 + '\2'?` 这个替换的正则表达式用 ? 代替了 /，\1 和 \2 代表引用，引用相应的分组

