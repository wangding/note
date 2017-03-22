# vim

模式化的编辑器。

- [官网](http://www.vim.org/)  
- [插件](http://www.vim.org/scripts/script_search_results.php?order_by=rating)  

## 学习资料

- http://www.jianshu.com/p/a361ce8c97bc
- vim 练级攻略：https://globalinheart.wordpress.com/2011/09/07/简明-vim-练级攻略/  

## 基本模式

- 编辑模式
- 插入模式
- 命令模式

## 打开文件

- vim [option] [file]
- +# 打开文件后，光标处于第#行的行首
- +/pattern 打开文件后，直接让光标处于第一个被/pattern匹配到的行的行首
- +打开文件后，在尾行追加

## 模式转换

- 编辑模式：默认模式
- 编辑模式-->输入模式

   - i：insert 在光标所在处输入
   - a：append 在光标的处后方输入
   - o：在光标所在处的下方打开一个新行
   - I：在光标所在行的行首输入
   - A：在光标所在行的行尾输入
   - O：在光标所在处的上方打开一个新行

- 输入模式-->编辑模式：ESC
- 编辑模式-->命令模式：:
- 命令模式-->编辑模式：ESC

## 关闭文件

- ZZ 保存并退出
- :q 退出，前提文件没有修改
- :q! 强制退出，不保存此前的修改
- :wq 保存并退出
- :x 保存并退出
- :w /path/file 另存为

## 光标跳转

- 字符间跳转
- h, l, 左右
- j, k, 上下
- #cmd 跳#个字符
- 单词间跳转
- w, 下一个单词的词首
- e,
- b,
- 行首尾跳转
- 行间跳转
- 句间跳转
- 段间跳转

## 窗口滚动

- ctrl-d 窗口向下滚动半屏
- ctrl-u 窗口向上滚动半屏
- ctrl-e 窗口向下滚动一行
- ctrl-y 窗口向上滚动一行
- ctrl-b 窗口向上滚动一页
- ctrl-f 窗口向下滚动一页
- zz     当前行位于屏幕窗口中间
- zt     当前行位于屏幕窗口顶部
- zb     当前行位于屏幕窗口底部
 
## 多窗口操作

- vim -o file1 file2 (水平分隔)  
- vim -O file1 file2 (垂直分隔)  
- :sp filename (水平分隔窗口，编辑文件)  
- :vs filename (垂直分隔窗口，编辑文件)  
- 关闭分割窗口 :q  
- 切换窗口 切换到普通模式下 ctrl + w w  

## 撤销操作

- u 撤销操作
- ctrl-r 恢复撤销

## 光标位置跳转

- ctrl-O 执行后退
- ctrl-I 执行前进
- ngg or nG 光标跳转的第 n 行
- :n 命令模式跳转到第 n 行

## vim 设置

- 显示行号：set number

## 执行命令

- :!command
- :!bash  创新启动一个 bash 执行命令，而没有退出 vim，执行完命令后 exit 回到 vim
- :r !command  讲命令运行的结果插入到当前行的下一行
- :n,m !command 起始行号 n 到结束行号 m 之间的内容，用 command 来处理。例如：:2,4 !sort
- 

## 复制

- yy 复制一行
- 

## 查找替换

- :s/old/new 替换行中首次出现的 old 为 new
- :s/old/new/g 替换行中所有 old 为 new
- :n,m s/old/new/g 用 new 替换 从 n 行到 m 行中的所有 old
- :%s/old/new/g 全文查找 old 替换成 new
- g 后跟 c 进行替换前的确认

## 命令模式常用命令

- :open file 打开文件 file
- :bn 下一个文件
- :bp 上一个文件
- Ctrl + 6 下一个文件

