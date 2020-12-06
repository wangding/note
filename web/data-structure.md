# 数据结构 JavaScript 版

## 栈

- javascrip 的数组，是数据结构里的顺序栈，支持 push 和 pop 操作
- `let a = []`，初始化一个空栈
- `a.push(2)`，压栈
- `a.pop())`，出栈

- 栈的应用
- 题目：括号的最大嵌套深度，来自 leetcode
- https://leetcode-cn.com/problems/maximum-nesting-depth-of-the-parentheses/

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var maxDepth = function(s) {
  const chars = s.split('');

  let nums=[], stack=[];
  for(let i=0, num=0; i<chars.length; i++) {
    if(chars[i] === '(') {
      stack.push('(');
      if(stack.length > num) num++;
    }

    if(chars[i] === ')') {
      stack.pop();
      if(stack.length === 0) {
        nums.push(num);
        num = 0;
      }
    }
  }

  return (nums.length === 0) ? 0 : Math.max(...nums);
};
```

## 队列

- javascrip 的数组，是数据结构里的顺序队列，支持队列操作
- `let a = []`，初始化一个空队列
- `a.push(2)`，进队
- `a.shift()`，出队

## 二叉树

- Huffman 编码
- `for(let i=0; i<NNUM_MAX; i++) hfmTree[i] = {l: 0, r: 0, p: 0, w: 0};`
