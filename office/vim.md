# vim﻿

模式化的编辑器。

- [官网](http://www.vim.org/)  
- [插件](http://www.vim.org/scripts/script_search_results.php?order_by=rating)  

## 学习资料

- http://www.jianshu.com/p/a361ce8c97bc
- vim 练级攻略：https://globalinheart.wordpress.com/2011/09/07/简明-vim-练级攻略/  

## 基本模式

* 编辑模式

* 输入模式，插入模式

* 末行模式，命令模式

## 打开文件

* vim [option] [file]

* +# 打开文件后，光标处于第#行的行首

* +/pattern 打开文件后，直接让光标处于第一个被/pattern匹配到的行的行首

* +打开文件后，在尾行追加

## 模式转换

* 编辑模式：默认模式

* 编辑模式-->输入模式

   * i：insert 在光标所在处输入

   * a：append 在光标的处后方输入

   * o：在光标所在处的下方打开一个新行

   * I：在光标所在行的行首输入

   * A：在光标所在行的行尾输入

   * O：在光标所在处的上方打开一个新行

* 输入模式-->编辑模式

  * ESC

* 编辑模式-->末行模式

  * ：

* 末行模式-->编辑模式

  * ESC

## 关闭文件

* ZZ 保存并退出

* :q 退出，前提文件没有修改

* :q! 强制退出，不保存此前的修改

* :wq 保存并退出

  * :w  :q

* :x 保存并退出

* :w /path/file 另存为

## 光标跳转

* 字符间跳转

* h, l, 左右

* j, k, 上下

* #cmd 跳#个字符

* 单词间跳转

* w, 下一个单词的词首

* e,

* b,

* 行首尾跳转

* 行间跳转

* 句间跳转

* 段间跳转