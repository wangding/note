# Markdown 基本语法

本文展示 Markdown 的基本语法，每小节下有两部分内容：效果展示和 Markdown 语法。

**目录**

- [标题](#标题)
- [段落](#段落)
- [换行](#换行)
- [强调](#强调)
- [行内代码](#行内代码)
- [文本块](#文本块)
- [列表](#列表)
  - [无序列表](#无序列表)
  - [有序列表](#有序列表)
  - [列表同构嵌套](#列表同构嵌套)
  - [列表异构嵌套](#列表异构嵌套)
- [分割线](#分割线)
- [图片](#图片)
- [链接](#链接)
  - [外部链接](#外部链接)
  - [内部链接](#内部链接)
  - [图片链接](#图片链接)
- [引用](#引用)

## 标题

**效果**

- 一级标题，见本文第一行标题：“Markdown 基本语法”
- 二级标题，见下一节标题：“3. 段落”
- 三级标题，见第 5 节标题：“5.1. 无序列表”
- 四级标题及以下：略

**语法**

- 在标题文字前加一个或多个 `#` 和空格
- `#` 号数量对应标题的级数

<pre>
# 一级标题文字
## 二级标题文字
### 三级标题文字
#### 四级标题文字
##### 五级标题文字
###### 六级标题文字
</pre>

- 或者在标题文字下方加两个以上 `=` 和 `-`
- 仅支持一级和二级两种标题

<pre>
一级标题文字
===========

二级标题文字
-----------
</pre>

## 段落

**效果**

这是一段普通文本段落。

**语法**

<pre>
这是一段普通文本段落。
</pre>

## 换行

**效果**

这是第一行。

这是第二行。

**语法**

- 两行文字中间间隔一个空行

<pre>
这是第一行。

这是第二行。
</pre>

- 或者在一行文字的末尾加两个空格，选中“这是第一行”文字来观察行末空格。

<pre>
这是第一行。  
这是第二行。  
</pre>

## 强调

- 强调是指文字的加粗和倾斜样式
- 斜体和粗体可混合使用
- 效果和语法见下面的表格

|效果|语法|
|----|-----|
|*斜体1*|`*斜体1*`|
|_斜体2_|`_斜体2_`|
|**粗体1**|`**粗体1**`|
|__粗体2__|`__粗体2__`|
|***斜粗体1***|`***斜粗体1***`|
|___斜粗体2___|`___斜粗体2___`|

## 行内代码

**效果**

JavaScript 通过 `console.log` 方法实现打印输出。

**语法**

- 用一对反引号（\`）包围行内的代码文字

<pre>
JavaScript 通过 `console.log` 方法实现打印输出。
</pre>

## 文本块

**效果**

    普通文本
    文本块
    文字高亮

** 语法**

- 在连续几行的文本开头加入 1 个 Tab 或者 4 个空格

<pre>
    普通文本
    文本块
    文字高亮
</pre>

- 或使用一对三个反引号（\`\`\`）包围文本

<pre>
```
普通文本
文本块
文字高亮
```
</pre>

## 列表

### 无序列表

**效果**

- HTML
* CSS
+ JavaScript

**语法**

- 在列表项文字前添加 `-` 和空格

<pre>
- HTML
- CSS
- JavaScript
</pre>

- 或者在列表项文字前添加 `*` 和空格

<pre>
* HTML
* CSS
* JavaScript
</pre>

- 或者在列表项文字前添加 `+` 和空格

<pre>
+ HTML
+ CSS
+ JavaScript
</pre>

- 或者在列表项文字前混合使用 `-, *, +` 和空格

<pre>
- HTML
* CSS
+ JavaScript
</pre>

### 有序列表

**效果**

1. HTML
1. CSS
1. JavaScript

**语法**

- 在列表项文字前添加数字、小数点和空格
- 数字可以连续编号，也可以不连续编号

<pre>
1. HTML
1. CSS
1. JavaScript
</pre>

### 列表同构嵌套

**效果**

- First item
- Second item
- Third item
    - Indented item
    - Indented item
- Fourth item


1. First item
2. Second item
3. Third item
    1. Indented item
    2. Indented item
4. Fourth item

**语法**

- 一列列表和二级列表是同种列表
- 下一级列表文字，缩进四个空格

<pre>
- First item
- Second item
- Third item
    - Indented item
    - Indented item
- Fourth item


1. First item
2. Second item
3. Third item
    1. Indented item
    2. Indented item
4. Fourth item
</pre>

### 列表异构嵌套

**效果**

- First item
- Second item
- Third item
    1. Indented item
    2. Indented item
- Fourth item



1. This is the first list item.
2. Here's the second list item.

    I need to add another paragraph below the second list item.

3. And here's the third list item.

**语法**

- 无序列表和有序列表可以混合嵌套
- 列表中可以嵌入其他内容
- 为了不打断列表编号，嵌套的内容最好前导 4 个空格缩进

<pre>
- First item
- Second item
- Third item
    1. Indented item
    2. Indented item
- Fourth item



1. This is the first list item.
2. Here's the second list item.

    I need to add another paragraph below the second list item.

3. And here's the third list item.
</pre>

## 分割线

**效果**

---

**语法**

- 下面三种语法，都可显示横线效果

<pre>
***
---
___
</pre>

## 图片

**效果**

![百度 logo](http://www.baidu.com/img/bdlogo.gif "百度 logo")

**语法**

<pre>
![alt](url title)
eg. ![百度 logo](http://www.baidu.com/img/bdlogo.gif "百度 logo")
</pre>

- `alt` 表示图片显示失败时的替换文本，可以省略
- `title` 表示鼠标悬停在图片时的显示文本（注意 title 周围要加双引号），可以省略
- `url` 图片的 url 地址

## 链接

### 普通链接

**效果**

[关于我](http://i.wangding.co)

**语法**

<pre>
[link-text](url)
eg. [关于我](http://i.wangding.co)
</pre>

- `link-text` 是链接文字
- `url` 是链接的网址

### 地址链接

**效果**

<http://i.wangding.co>

**语法**

```
<http://i.wangding.co>
等价于：[http://i.wangding.co](http://i.wangding.co)
```

### 链接引用

**效果**

[关于我][1]

**语法**

- 由链接文字和引用两部分组成
- 通常在文章中出现多次重复的链接时比较有用
- url 地址只出现一次，方便文档的修改维护
- 通常引用部分置于文章的末尾

<pre>
[link-text][link-ref]
[link-ref]: url

eg.
[关于我][1]
[1]: http://i.wangding.co
</pre>

### 带格式的链接

**效果**

**[关于我][1]**

*[关于我][1]*

**语法**

```
**[关于我][1]**

*[关于我][1]*
```

### 内部链接

**效果**

[回到顶部](#markdown-基本语法)

**语法**

- 内部链接点击后在当前文档内部跳转
- 外部链接点击后会打开其他网站

<pre>
[link-text](#hash)
eg. [回到顶部](#markdown-基本语法)
</pre>

### 图片链接

**效果**

[![](http://www.baidu.com/img/bdlogo.gif)](http://www.baidu.com)

**语法**

- 在链接 link-text 的 `[]` 中嵌入图片的语法

<pre>
[![](http://www.baidu.com/img/bdlogo.gif)](http://www.baidu.com)
</pre>

## 引用

### 引用文本

**效果**

> Metaprogramming is a programming technique in which computer programs have the ability to treat other programs as their data. It means that a program can be designed to read, generate, analyze or transform other programs, and even modify itself while running. In some cases, this allows programmers to minimize the number of lines of code to express a solution, in turn reducing development time. It also allows programs a greater flexibility to efficiently handle new situations without recompilation.

**语法**

- 在引文前添加一个大于号 `>` 和空格

<pre>
> Metaprogramming is a programming technique in which computer programs have the ability to treat other programs as their data. It means that a program can be designed to read, generate, analyze or transform other programs, and even modify itself while running. In some cases, this allows programmers to minimize the number of lines of code to express a solution, in turn reducing development time. It also allows programs a greater flexibility to efficiently handle new situations without recompilation.
</pre>

### 嵌套块引用

**效果**

> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

**语法**

- 一级块引用前加一个大于号 `>` 和空格
- 二级快引用前加两个大于号 `>>` 和空格
- 三级块引用以此类推

<pre>
> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.
</pre>

### 块引用中的格式

**效果**

> #### The quarterly results look great!
>
> - Revenue was off the chart.
> - Profits were higher than ever.
>
> *Everything* is going according to **plan**.

**语法**

<pre>
> #### The quarterly results look great!
>
> - Revenue was off the chart.
> - Profits were higher than ever.
>
> *Everything* is going according to **plan**.
</pre>

[1]: http://i.wangding.co
