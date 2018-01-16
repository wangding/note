# JavaScript 学习笔记

内容和目录主要摘自《JavaScript 编程精解》，用《JavaScript 忍者秘籍》的内容来补充。

## 第 1 章 JavaScript 基础：值、变量、控制流程

六种基本类型：
- number 数字  
  - 数字是用 64 位的浮点数表示的  
  - 其中 1 位表示符号位  
  - 11 位表示小数  
  - 剩下 52 位表示整数  
  - 可以表示 2^52 以内的任何整数  
  - 运算符包括：`+、-、*、/、%`  
- string 字符串  
  - 不像 C 语言，没有字符类型  
  - 单引号和双引号都可以，但是需前后一致  
  - `\` 表示转义，`\n` 表示换行  
  - `+` 可以连接字符串  
- boolean 布尔值  
- object 对象  
- function 函数  
- undefined  

下面的程序用来验证六种基本类型。

```javascript
console.log(typeof 3.14);
console.log(typeof true);
console.log(typeof '3.14');
console.log(typeof { 'key': 3.14 });
console.log(typeof Object);
console.log(typeof undefine);
console.log(typeof null);
```


类型转换：
- 隐式（自动）类型转换  
- 显示（手动）类型转换  


运算符：
- 一元运算符
  - 只有一个参与运算的值  
  - `typeof` 求值的类型  
  - `!` 取反，一元逻辑运算符  
- 二元运算符
  - 有两个参与运算的值  
  - `+、-、*、/、%` 都是二元算术运算符  
  - `>、<、>=、<=、==、===、!=、!===` 都是二元关系运算符  
  - `&&、||` 都是二元逻辑运算符  
  - `+=、-=、/=、*=、%=、++、--` 组合运算符或快捷运算符  
- 三元运算符


值或变量 + 运算符 => （构成）表达式或语句


变量：
- 变量名不可以是关键字与保留字  
- 变量名区分大小写  


函数：
- 函数名跟变量名命名规则类似  
- 对象中的函数也成为方法  
- 函数有入口参数和返回值  


程序结构：
- 顺序结构  
- 分支结构  
  - `if-else` 判断  
  - `switch-case` 判断  
- 循环结构  
  - `while` 循环  
  - `for`  循环  
  - `do-while`  循环  
  - `foreach` 循环  
  - `break` 跳出循环  
  - `continue` 跳过循环  


注释：
- `//` 行注释以及半行注释  
- `/*  */` 块注释  


## 第 2 章 函数

函数的语法：
- 函数名  
  - 可以没有，则为匿名函数  
- 入口参数  
  - 可以没有  
  - 可以是可变参数，用 arguments 数组访问  
  - 默认参数需要自己写代码实现  
- 函数体  
- 返回值  
  - 可以没有 `return 表达式`，则返回 `undefine`  

定义函数的最基本形式，代码举例：

```javascript
function square(x) {
  return x * x;
}
```

函数的用法；
- 函数调用的代码可以出现在函数定义之前  
- 函数内部变量的作用域是局部的  
- 函数内部变量的作用域是嵌套的  
- JavaScript 没有块作用域，函数是唯一创造局部作用域的工具  
- 递归函数  
- 立即执行函数  
- 函数的调用或者执行，是通过 `()` 来实现的  
- 没有 `()` 的函数名，是一个函数类型的值或者变量  
- 闭包：包裹一个局部变量的函数



## 第 3 章 数据结构：对象和数组


## 第 4 章 错处处理


## 第 5 章 函数式编程


## 第 6 章 面向对象编程


## 第 7 章 模块化

## 第 8 章 正则表达式

## 第 9 章 Web 编程：速成课

## 第 10 章 文档对象模型

## 第 11 章 浏览器事件

## 第 12 章 HTTP 请求


## 第 1 章 进入忍者世界

一个 JavaScript 库的组成可以分为如下三个方面：
- JavaScript 语言的高级使用  
  - JavaScript 中，对象、函数和闭包之间有着密切的关系（如图 1.1 所示）  
  - 还有两个 JavaScript 特性远远未被充分利用：定时器和正则表达式  
  - 定时器可以让我们有能力解决复杂的编码任务，如：长时间运行的计算和平滑的动画  
  - 正则表达式可以简化原本相当复杂的代码  
- 跨浏览器代码的精心构建  
  - 桌面浏览器市场份额和开发成本分析，如图 1.2 所示  
  - 移动浏览器市场份额和开发成本分析，如图 1.3 所示  
  - 数据来源：http://gs.statcounter.com
- 当前能够聚众合一的最佳实践应用  
  - 测试  
  - 性能分析  
  - 调试技巧  

书上关于性能分析的代码片段，如下：
```javascript
start = new Date().getTime();
for(var n = 0; n < maxCount; n++) {
  // perform the operation to be meassured
}
elapsed = new Date().getTime();
console.log('Messured Time: %s ms', elapsed);
```

其实这个代码片段完全可以用 `console.time()` 和 `console.timeEnd()` 方法来实现。代码如下：
```javascript
console.time('TASK-ABC');
for(var n = 0; n < maxCount; n++) {
  // perform the operation to be meassured
}
console.timeEnd('TASK-ABC');
```

## 第 2 章 利用测试和调试武装自己

调试的方法和手段，参考 Node.js 应用开发（中篇）调试的教案。
前端代码的调试，主要是使用 Chrome 浏览器的开发者工具，断点交互调试以及 `coonsole.log()` 的打印调试。

测试框架




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

【参考资料】  

- JSDoc 文档资料: http://www.css88.com/doc/jsdoc/index.html  
- JSDoc 工具下载: https://www.npmjs.com/package/jsdoc
- JSDoc 的 vim 插件的内容，参考：vim.md  
- JavaScript 编码规范：https://standardjs.com/readme-zhcn.html
