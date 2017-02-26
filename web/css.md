# CSS 技术

CSS 的层次：
- 基本样式：背景色，文字颜色，字体，最简单的选择器；
- 选择器、布局、定位；
- CSS3 的动画特效等；
- bootstrap；（看了看 github 是 sass 的代码）
- less 或 sass；（less 曾亮有课，sass 也有课）

## CSS 基础

### CSS 简介

- CSS 指层叠样式表 (Cascading Style Sheets)
- 样式定义如何显示 HTML 元素
- 样式通常存储在样式表中
- 把样式添加到 HTML 4.0 中，是为了解决内容与表现分离的问题
- 外部样式表可以极大提高工作效率
- 外部样式表通常存储在 CSS 文件中
- 多个样式定义可层叠为一

#### 样式解决了一个普遍的问题

HTML 标签原本被设计为用于定义文档内容。通过使用 `<h1>、<p>、<table>` 这样的标签，HTML 的初衷是表达“这是标题”、“这是段落”、“这是表格”之类的信息。同时文档布局由浏览器来完成，而不使用任何的格式化标签。

由于两种主要的浏览器（Netscape 和 Internet Explorer）不断地将新的 HTML 标签和属性（比如字体标签和颜色属性）添加到 HTML 规范中，创建文档内容清晰地独立于文档表现层的站点变得越来越困难。

为了解决这个问题，万维网联盟（W3C），这个非营利的标准化联盟，肩负起了 HTML 标准化的使命，并在 HTML 4.0 之外创造出样式（Style）。

所有的主流浏览器均支持层叠样式表。

#### 样式表极大地提高了工作效率

样式表定义如何显示 HTML 元素，就像 HTML 3.2 的字体标签和颜色属性所起的作用那样。样式通常保存在外部的 .css 文件中。通过仅仅编辑一个简单的 CSS 文档，外部样式表使你有能力同时改变站点中所有页面的布局和外观。

由于允许同时控制多重页面的样式和布局，CSS 可以称得上 WEB 设计领域的一个突破。作为网站开发者，你能够为每个 HTML 元素定义样式，并将之应用于你希望的任意多的页面中。如需进行全局的更新，只需简单地改变样式，然后网站中的所有元素均会自动地更新。

#### 多重样式将层叠为一个

样式表允许以多种方式规定样式信息。样式可以规定在单个的 HTML 元素中，在 HTML 页的头元素中，或在一个外部的 CSS 文件中。甚至可以在同一个 HTML 文档内部引用多个外部样式表。
层叠次序

当同一个 HTML 元素被不止一个样式定义时，会使用哪个样式呢？

一般而言，所有的样式会根据下面的规则层叠于一个新的虚拟样式表中，其中数字 4 拥有最高的优先权。

1. 浏览器缺省设置
2. 外部样式表
3. 内部样式表（位于 <head> 标签内部）
4. 内联样式（在 HTML 元素内部）

因此，内联样式（在 HTML 元素内部）拥有最高的优先权，这意味着它将优先于以下的样式声明：<head> 标签中的样式声明，外部样式表中的样式声明，或者浏览器中的样式声明（缺省值）。

### CSS 基础语法

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明。

```css
selector {declaration1; declaration2; ... declarationN }
```

选择器通常是您需要改变样式的 HTML 元素。

每条声明由一个属性和一个值组成。

属性（property）是您希望设置的样式属性（style attribute）。每个属性有一个值。属性和值被冒号分开。

```css
selector {property: value}
```

下面这行代码的作用是将 h1 元素内的文字颜色定义为红色，同时将字体大小设置为 14 像素。

在这个例子中，h1 是选择器，color 和 font-size 是属性，red 和 14px 是值。

```css
h1 {color:red; font-size:14px;}
```

下面的示意图为您展示了上面这段代码的结构：  
![CSS 语法](http://www.w3school.com.cn/i/ct_css_selector.gif)

提示：请使用花括号来包围声明。

---
#### 值的不同写法和单位

除了英文单词 red，我们还可以使用十六进制的颜色值 #ff0000：

```css
p { color: #ff0000; }
```

为了节约字节，我们可以使用 CSS 的缩写形式：

```css
p { color: #f00; }
```

我们还可以通过两种方法使用 RGB 值：

```css
p { color: rgb(255,0,0); }
p { color: rgb(100%,0%,0%); }
```

请注意，当使用 RGB 百分比时，即使当值为 0 时也要写百分比符号。但是在其他的情况下就不需要这么做了。比如说，当尺寸为 0 像素时，0 之后不需要使用 px 单位，因为 0 就是 0，无论单位是什么。

---
#### 记得写引号

提示：如果值为若干单词，则要给值加引号：
```css
p {font-family: "sans serif";}
```

#### 多重声明：

提示：如果要定义不止一个声明，则需要用分号将每个声明分开。下面的例子展示出如何定义一个红色文字的居中段落。最后一条规则是不需要加分号的，因为分号在英语中是一个分隔符号，不是结束符号。然而，大多数有经验的设计师会在每条声明的末尾都加上分号，这么做的好处是，当你从现有的规则中增减声明时，会尽可能地减少出错的可能性。就像这样：
```css
p {text-align:center; color:red;}   
```
你应该在每行只描述一个属性，这样可以增强样式定义的可读性，就像这样：
```css
p {
  text-align: center;
  color: black;
  font-family: arial;
}
```
#### 空格和大小写

大多数样式表包含不止一条规则，而大多数规则包含不止一个声明。多重声明和空格的使用使得样式表更容易被编辑：
```css
body {
  color: #000;
  background: #fff;
  margin: 0;
  padding: 0;
  font-family: Georgia, Palatino, serif;
  }
```
是否包含空格不会影响 CSS 在浏览器的工作效果，同样，与 XHTML 不同，CSS 对大小写不敏感。不过存在一个例外：如果涉及到与 HTML 文档一起工作的话，class 和 id 名称对大小写是敏感的。



### CSS 高级语法
### CSS 派生选择器
### CSS id 选择器
### CSS 类选择器
### CSS 属性选择器
### CSS 创建

## CSS 样式

- CSS 背景
- CSS 文本
- CSS 字体
- CSS 链接
- CSS 列表
- CSS 表格
- CSS 轮廓

## CSS 盒模型

- CSS 框模型概述
- CSS 内边距
- CSS 边框
- CSS 外边距
- CSS 外边距合并

## CSS 定位

- CSS 定位概述
- CSS 相对定位
- CSS 绝对定位
- CSS 浮动

## CSS 选择器

- CSS 元素选择器
- CSS 选择器分组
- CSS 类选择器详解
- CSS ID 选择器详解
- CSS 属性选择器详解
- CSS 后代选择器
- CSS 子元素选择器
- CSS 相邻兄弟选择器
- CSS 伪类
- CSS 伪元素

## CSS 高级

- CSS 对齐
- CSS 尺寸
- CSS 分类
- CSS 导航栏
- CSS 图片库
- CSS 图片透明
- CSS 媒介类型
- CSS 注意事项
- CSS 总结



## CSS 选择器语法

http://www.w3school.com.cn/cssref/css_selectors.asp  





## CSS 实战

- stylish 火狐插件  
- 分享 stylish 作品  
- 百度案例：https://www.zhihu.com/question/36540171
- https://www.zhihu.com/search?type=content&q=stylish
- CSS 画图标
  - 视频：慕课网，重拾CSS的乐趣
  - 作品：http://www.oschina.net/news/52103/50-css-only-icon-graphics
  - 极客：http://one-div.com/
  - 