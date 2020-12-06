# JavaScript 进阶

## 基本语法

### if 判断

- 把简单的 if 判断，改成三目运算
- 优点：
- 代码简洁
- 缺点：
- 代码比较长，不如 if 语句直观

```javascript
// 修改之前
for(let i=0; i<SNUM_MAX; i++) {
  if(freq[i] > max)  max = freq[i];
}

// 修改之后
freq.forEach(f => max = (f > max) ? f : max);
```

- 把简单的 if 判断，变成与运算
- 优点：
- 代码简洁
- 缺点：
- 降低了代码的可读性

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
- 优点：
- 可以更早的垃圾回收
- 可以减少循环变量之间的干扰
- 缺点：
- 循环体外，不能再访问循环变量

```javascript
// 修改之前
let i;
for(i=0; i<NNUM_MAX; i++) hfmTree[i] = {l: 0, r: 0, p: 0, w: 0};

// 修改之后
for(let i=0; i<NNUM_MAX; i++) hfmTree[i] = {l: 0, r: 0, p: 0, w: 0};
```

- 把循环体中用到的临时变量，定义到 for 语句中
- 优点：
- 代码简洁
- 缺点：
- 循环体外，不能再访问循环体内部变量

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
- 优点：
- 代码简洁
- 缺点：
- 不能访问循环变量

```javascript
// 修改之前
for(let i=0; i<srcData.length; i++) freq[srcData[i]]++;

// 修改之后
srcData.forEach(data => freq[data]++);
```

- 把循环体内变量的定义，放到循环体外面
- 优点：
- 避免频繁分配内存
- 缺点：
- 扩大的变量的作用域
- 可能导致变量之前的干扰

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

## return 语句

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
