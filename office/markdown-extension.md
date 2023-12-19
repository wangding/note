# Markdown 扩展语法

本文展示 Markdown 的扩展语法，每小节下有两部分内容：效果展示和 Markdown 语法。

**目录**

- [代码块](#代码块)
- [表格](#表格)
- [表情](#表情)
- [diff 语法](#diff-语法)

## 代码块

**效果**

```c
int main(int argc, char *argv[]) {
  printf("hello c");
  return 0;
}
```

**语法**

- 用三个反引号（\`\`\`）包围代码块

<pre>
```lang
code
```
eg.
```c
int main(int argc, char *argv[]) {
  printf("hello c");
  return 0;
}
```
</pre>

- `lang` 是语言的名称，如：`c`, `bash`, `javascript`, 等
- `code` 是代码

## 表格

**效果**

| 左对齐 | 居中  | 右对齐 |
| :--- | :---: | ---: |
| col 3 is | some wordy text | $1600 |
| col 2 is | centered | $12 |
| zebra stripes | are neat | $1 |


**语法**

- 单元格被左右两侧竖线包围，同一列中单元格的竖线不要求对齐
- 一定要有表头的分割线
- 表头的分割线通过冒号（`:`）设置单元格对齐
- 左对齐、右对齐，对应冒号（`:`）在分割线的左或者右
- 居中对齐对应分割线被左右两个冒号包围
- 默认左对齐，可以没有冒号
- 分割线是三个以上的横线字符（`-`）
- 不支持单元格合并

<pre>
| 左对齐 | 居中  | 右对齐 |
| :--- | :---: | ---:|
| col 3 is | some wordy text | $1600 |
| col 2 is | centered | $12 |
| zebra stripes | are neat | $1 |
</pre>

## 表情

**效果**

:blush:

**语法**

<pre>
:emoji:
</pre>

- `emoji` 是表情符号的代码
- 例如：表情符号： :blush: ，对应的代码是 `:blush:`
- 所有的 `emoji` 代码在[这里](./emoji.md)

## diff 语法

版本控制的系统中都少不了 diff 的功能，即展示一个文件内容的增加与删除。

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

- 与代码块类似，只是在三个反引号后面写 diff
- `+ `开头表示新增
- `- `开头表示删除
- 另外还有有 `!` 和 `#`
