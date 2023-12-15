# Markdown 扩展语法

本文展示 Markdown 的扩展语法，每小节下有两部分内容：效果展示和 Markdown 语法。

**目录**

- [代码块](#代码块)
- [表格](#表格)
- [表情](#表情)
- [diff语法](#diff-语法)

## 代码块

**效果**

```c
int main(int argc, char *argv[]) {
  printf('hello c');
  return 0;
}
```

```bash
echo "hello bash"
```

```javascript
console.log('hello JavaScript');
```

**语法**

<pre>
```lang
code
```
eg.
```javascript
console.log('hello JavaScript');
```
</pre>

- `lang` 是语言的名称，如：`c`, `bash`, `javascript`, 等
- `code` 是代码

## 表格

**效果**

| 左对齐 | 居中  | 右对齐 |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |


**语法**

<pre>
| 左对齐 | 居中  | 右对齐 |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |
</pre>

## 表情

**效果**

:blush:

**语法**

<pre>
:emoji:
eg. :blush:
</pre>

- `emoji` 是表情符号的描述符，所有的 `emoji` 描述符在[这里](./emoji.md)

## diff 语法

版本控制的系统中都少不了 diff 的功能，即展示一个文件内容的增加与删除。

GFM 中可以显示的展示 diff 效果。使用绿色表示新增，红色表示删除。

**效果**

```diff
+ 人闲桂花落，
- 夜静春山空。
! 月出惊山鸟，
# 时鸣春涧中。
```

**语法**

<pre>
```diff
+ 人闲桂花落，
- 夜静春山空。
! 月出惊山鸟，
# 时鸣春涧中。
```
</pre>

- 与代码高亮类似，只是在三个反引号后面写 diff
- `+ `开头表示新增
- `- `开头表示删除
- 另外还有有 `!` 和 `#`
