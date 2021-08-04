# JavaScript

## 基本语法

### if 判断

- 把简单的 if 判断，改成三目运算
- 优点：代码简洁
- 缺点：代码比较长，不如 if 语句直观

```javascript
// 修改之前
for(let i=0; i<SNUM_MAX; i++) {
  if(freq[i] > max)  max = freq[i];
}

// 修改之后
freq.forEach(f => max = (f > max) ? f : max);
```

- 把简单的 if 判断，变成与运算
- 优点：代码简洁
- 缺点：降低了代码的可读性

```javascript
// 修改之前
for(let i=0, num=0; i<SNUM_MAX; i++) {
  if(freq[i] !== 0) printf(`x${++num} \t${i}\t${p[i]}\n`);
}

// 修改之后
for(let i=0, num=0; i<SNUM_MAX; i++) {
  (freq[i] !== 0) && printf(`x${++num} \t${i}\t${p[i]}\n`);
}
```

### for 循环

- 把循环变量定义在 for 语句块里，并使用 let 声明
- 优点：可以更早的垃圾回收；可以减少循环变量之间的干扰
- 缺点：循环体外，不能再访问循环变量

```javascript
// 修改之前
let i;
for(i=0; i<NNUM_MAX; i++) hfmTree[i] = {l: 0, r: 0, p: 0, w: 0};

// 修改之后
for(let i=0; i<NNUM_MAX; i++) hfmTree[i] = {l: 0, r: 0, p: 0, w: 0};
```

- 把循环体中用到的临时变量，定义到 for 语句中
- 优点：代码简洁
- 缺点：循环体外，不能再访问循环体内部变量

```javascript
// 修改之前
let num = 0;
for(let i=0; i<SNUM_MAX; i++) {
  if(freq[i] !== 0) {
    printf(`x${++num} \t${i}\t${freq[i]}\n`);
  }
}

// 修改之后
for(let i=0, num=0; i<SNUM_MAX; i++) {
  (freq[i] !== 0) && printf(`x${++num} \t${i}\t${p[i]}\n`);
}
```

- 把 for 循环改成 forEach
- 优点：代码简洁
- 缺点：不能访问循环变量

```javascript
// 修改之前
for(let i=0; i<srcData.length; i++) freq[srcData[i]]++;

// 修改之后
srcData.forEach(data => freq[data]++);
```

- 把循环体内变量的定义，放到循环体外面
- 优点：避免频繁分配内存
- 缺点：扩大的变量的作用域；可能导致变量之前的干扰

```javascript
// 修改之前
for(let i=0; i<runLen.length-1; i++) {
  let distance = runLen[i+1].pos - runLen[i].pos - runLen[i].len;
  if(distance < 3) {
    runLen[i].len += distance + runLen[i+1].len;
    runLen.splice(i+1, 1);
    i--;
  }
}

// 修改之后
let distance = 0;
for(let i=0; i<runLen.length-1; i++) {
  distance = runLen[i+1].pos - runLen[i].pos - runLen[i].len;
  if(distance < 3) {
    runLen[i].len += distance + runLen[i+1].len;
    runLen.splice(i+1, 1);
    i--;
  }
}
```

- 把 for 循环改成 map 调用
- 把 for 循环改成 reduce 调用
- 把 for 循环改成 filter 调用

### return 语句

- 把 if 判断，决定不同的返回值，改成三目运算符
- 优点：代码简洁
- 缺点：无

```javascript
// 修改之前
if(nums.length === 0) {
  return 0;
} else {
  return Math.max(...nums);
}

// 修改之后
return (nums.length === 0) ? 0 : Math.max(...nums);
```

### 类型判断

四种判断类型的方法：
1. typeof，缺点：不能判断对象类型 typeof [], typeof {}
2. constructor，可以找到变量是通过谁构造出来的 [].constructor ({}).constructor
3. instanceof，判断谁是谁的实例
4. Object.prototype.toString.call()，可以。但是缺点，不能判断谁是谁的实例

### 高阶函数 (high order function)

- 普通函数就是一阶函数
- 函数的函数就是二阶函数，即：高阶函数
- 函数的函数，有以下三种形态：
  - 函数的参数是函数（这个作为参数传入的函数，通常叫回调函数）。例如：Array.prototype.forEach()，Array.prototype.reduce()，Array.prototype.map()，Array.prototype.filter()
  - 函数的返回值是函数，外层函数对返回的函数形成一层包裹
  - 上面两者的混合
- 应用场景 1：扩展当前的业务代码，又不希望修改原函数，面向切面编程或代理模式

```javascript
Function.prototype.before = function(beforefn){
  let _self = this;    // 保存原函数的引用

  return function() {  // 返回包含了新函数和原函数的代理函数
    beforefn.apply(this, arguments);     // 执行新函数，修正this
    _self.apply(this, arguments);        // 执行原函数
  }
}

Function.prototype.after = function(afterfn){
  let _self = this;

  return function(){
    _self.apply(this, arguments);
    afterfn.apply(this, arguments);
  }
}

let func = function(){
  console.log(4)
}

// before 函数返回一个函数，取决于调用它的函数
func =  func.before(function(){
  console.log(1);
}).before(function() {
  console.log(2);
}).after(function(){
  console.log(7);
}).after(function() {
  console.log(8);
});
console.log(func.toString());
func();
```

- 应用场景二，柯里化。在计算机科学中，柯里化（英语：Currying）是把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术。
- 柯里化，可以理解为提前接收部分参数，延迟执行，不立即输出结果，而是返回一个接受剩余参数的函数。因为这样的特性，也被称为部分计算函数。柯里化，是一个逐步接收参数的过程。反柯里化，是一个泛型化的过程。它使得被反柯里化的函数，可以接收更多参数。目的是创建一个更普适性的函数，可以被不同的对象使用。有鸠占鹊巢的效果。

```javascript
// 类型判断的柯里化

console.log(isType('123', 'String'));
console.log(isType([], 'String'));

function isType(value, type) {
  return Object.prototype.toString.call(value) === `[object ${type}]`;
}

// 把 isType 方法细化为：isArray, isString，把两个参数变成一个参数

function isType2(type) {
  return function(value) {
    return Object.prototype.toString.call(value) === `[object ${type}]`;
  }
}

let isString = isType2('String');
let isArray  = isType2('Array');

console.log(isString('123'));
console.log(isString([]));
console.log(isArray([]));

// 通用的 currying

function sum(a, b, c, d, e, f) {
  return a + b + c + d + e + f;
}

console.log(sum(1,2,3,4,5,6));

// 改成:
// let sum = currying(sum)(1, 2)(3, 4)(5)(6)

function currying(fn, arr=[]) {
  let len = fn.length;

  return function(...arg) {
    arr = [...arr, ...arg];
    if(arr.length < len) {
      return currying(fn, arr);
    } else {
      return fn(...arr);
    }
  }
}

let sum2 = currying(sum)(1,2)(3,4)(5)(6);
console.log(sum2);
```

### 工厂函数

- 现实中的工厂生成产品，编程领域工厂的产品是对象
- 函数的返回值是对象，这种函数成为工厂函数
