# vim

模式化的编辑器。

- [官网](http://www.vim.org/)  
- [插件](http://www.vim.org/scripts/script_search_results.php?order_by=rating)  

## 学习资料

下面这些文章一篇一篇的搞定，学扎实了：

- http://www.jianshu.com/p/a361ce8c97bc
- vim 练级攻略：https://globalinheart.wordpress.com/2011/09/07/简明-vim-练级攻略/  
- 知乎 vim 专栏：https://zhuanlan.zhihu.com/hack-vim
- youtube 上大神的 vim 视频：https://www.youtube.com/playlist?list=PLwJS-G75vM7kFO-yUkyNphxSIdbi_1NKX
- 百度前端工程师的文章：http://efe.baidu.com/blog/vim-javascript-completion/
- **伯乐在线的 vim 文章（重点学习）**：http://blog.jobbole.com/tag/vim/

## 基本模式

- 编辑模式
- 插入模式
- 命令模式
- 可视模式

## 打开文件

- vim [option] [file]
- +# 打开文件后，光标处于第#行的行首
- +/pattern 打开文件后，直接让光标处于第一个被/pattern匹配到的行的行首
- +打开文件后，在尾行追加
- :e <path/to/file>  打开一个文件

## 模式转换

- 编辑模式：默认模式
- 编辑模式-->输入模式

   - i：insert 在光标所在处输入
   - a：append 在光标的处后方输入
   - o：在光标所在处的下方打开一个新行
   - cw: 替换光标所在位置单词
   - I：在光标所在行的行首输入
   - A：在光标所在行的行尾输入
   - O：在光标所在处的上方打开一个新行

- 输入模式-->编辑模式：ESC
- 编辑模式-->命令模式：:
- 命令模式-->编辑模式：ESC
- 默认模式-->可视模式：v 字符选择，V 行选择，ctrl+v 块选择

## 关闭文件

- ZZ 保存并退出
- :q 退出，前提文件没有修改
- :q! 强制退出，不保存此前的修改
- :wq 保存并退出
- :x 保存并退出
- :w /path/file 另存为
- :saveas <path/to/file> 另存为

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
- g; 跳到上一次修改的地方
- L 光标跳到屏幕下方

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
- ctrl w + 先按 ctrl w，然后再按 + ，放大窗口
- ctrl w - 先按 ctrl w，然后再按 -，缩小窗口
- :close 关闭窗口
- ctrl w j,k,l,m 切换到上下左右的窗口
- :Ex 开启目录浏览器，可以浏览目录的所有文件并选择打开
- :resize+num 把当前窗口增加 num 行
- :resize-num 把当前窗口减少 num 行
- :vertical resize+num 把当前窗口增加 num 列
- :vertical resize-num 把当前窗口减少 num 列
- :ls 显示所有打开的文档


## 撤销操作

- u 撤销操作
- ctrl-r 恢复撤销

## 光标位置跳转

- ctrl-O 执行后退
- ctrl-I 执行前进
- ngg or nG 光标跳转的第 n 行
- :n 命令模式跳转到第 n 行
- %  匹配括号
- * 和 # 匹配光标所在的单词，* 移到上一个匹配的单词处，# 移动到下一个单词处

## vim 设置

- 显示行号：set number

## 执行命令

- :!command
- :!bash  创新启动一个 bash 执行命令，而没有退出 vim，执行完命令后 exit 回到 vim
- :r !command  将命令运行的结果插入到当前行的下一行
- :n,m !command 起始行号 n 到结束行号 m 之间的内容，用 command 来处理。例如：:2,4 !sort
- 

## 复制和移动

- yy 复制一行

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
- :n1,n2 co n3 将 n1 到 n2 行的内容复制到 n3 行下
- :n1,n2 m m3 将 n1 到 n2 行的内容移动到 n3 行下
- :n1,n2 !command 将 n1 到 n2 行的内容作为 command 命令的输入并执行，执行的结果放到 n1 行的位置
- :n1,n2 d 将 n1 到 n2 行的内容删除

## 录制宏

- qa 启动录制宏 a
- 操作
- q 停止录制宏
- @a 或者 @@ 执行宏 a 或者执行最新的宏
- 100@@ 执行 100 次最近的宏

## 的区域对象操作

- i 代表 in
- a 代表 around
- 语法：<动作>i/a<对象范围>
  - 动作有：
    - v 选中
    - d 删除
    - y 复制
  - 区域范围有：
    - i 代表 in
    - a 代表 around
  - 对象范围有：
    - w 单词
    - s 句子
    - p 段落
    - 也可以是一些范围界定符号，例如：逗号，括号，等
  - 参考：http://blog.jobbole.com/18339

## 块操作

操作流程如下：
- ctrl-v 块的起始位置
- 向上或向下移动光标
- I 大写字母 I，代表行首插入操作
- 或者行尾操作，$，A，内容
- 插入的内容，如：空格或前导符 -
- ESC 退出插入操作，块的位置都会插入

## 代码缩进

操作流程如下：
- V 进入整行的可视操作模式
- 向上或向下移动光标
- < 或 > 进行左右缩进
- = 自动缩进，自动缩进就是把代码复制到其他的位置之后，使用自动缩进，一步把代码的缩进调整到位

## 相对行号

设置方法，set relativenumber
优势如下：
- 高效。如果代码比较长，比如当前的光标在 700 行处，因为跳转都是局部和小范围内的跳转，也就是在一个屏幕窗口的可是范围内跳转。使用绝对行号跳转是 705G，而使用相对行号就是 5j，可见敲击按键的次数少一些。
- 代码块操作。对一块连续的代码块进行复制或者缩进，等操作时，块的起始位置到终止位置光标的移动用相对行号会非常方便。跟上面的类似，例如：700 行处，V 整行选中作为代码块的起始行，705G作为代码块的终止行，这是绝对行号操作方式。而相对行号，V，5j，显然按键次数更少一些。
## vim 插件管理工具 Vundle

- 安装 Vundle
```bash
mkdir -p ~/.vim/bundle
cd ~/.vim/bundle
git clone https://github.com/VundleVim/Vundle.vim.git
```
- 配置 .vimrc
略

- 插件管理方法
  - 在 vim 应用中运行 :PluginInstall

## 打造 IDE

基本的文章参考：http://efe.baidu.com/blog/vim-javascript-completion/

- ternjs/tern_for_vim
- Valloric/YouCompleteMe
  - 安装：使用 Vundle 下载 YCM 插件
  - 在 YCM 文件夹下执行 install.py --tern-completer
  - 配置 .vimrc 的 <leader>-gf 跳转到定义处
- jiangmiao/auto-pairs

  - https://github.com/vim-syntastic/syntastic
  - 语法检查，**没有搞定**

## 键盘映射

- 有待补充

## 杂项

- :source ~/.vimrc 不退出 vim 重新加载配置文件

