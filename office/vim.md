# vim 笔记

模式化编辑器

## 打开文件

- vim [option] [file]
- `:e <path/to/file>` 打开一个文件
- `:e` 刷新或重载当前的文件
- `:e!` 如果当前文件缓存有变化 `:e!` 放弃变更
- `e` 是 `edit` 的缩写，编辑文件

## 转换模式

模式种类：
- 编辑模式：默认模式
- 输入模式
- 命令模式
- 可视模式（块选模式）

模式转换：
- 输入模式-->编辑模式：ESC
- 编辑模式-->命令模式：:
- 命令模式-->编辑模式：ESC
- 默认模式-->可视模式：v 字符选择，V 行选择，ctrl+v 块选择
- 编辑模式-->输入模式
   - i：insert 在光标所在处输入
   - a：append 在光标的处后方输入
   - o：在光标所在处的下方打开一个新行
   - cw: 替换光标所在位置单词
   - I：在光标所在行的行首输入
   - A：在光标所在行的行尾输入
   - O：在光标所在处的上方打开一个新行

## 关闭文件

- ZZ 保存并退出
- :q 退出，前提文件没有修改
- :q! 强制退出，不保存此前的修改
- :wq 保存并退出
- :x 保存并退出
- :w /path/file 另存为
- :saveas `<path/to/file>` 另存为

## 跳转光标

- 字符间跳转
  - h, l, 左右
  - j, k, 上下
  - `#cmd` 跳 `#` 个字符
- 单词间跳转
  - w, 下一个单词的词首
  - e, 光标向前移动到词尾
  - b, 光标向后移动到词首
  - `#cmd` 跳 `#` 个单词
- 行首尾跳转
  - 0 行首
  - ^ 非空白行首
  - $ 行尾
- 行间跳转
  - gg, 1G 到首行
  - G 到末行
  - nG, ngg 到第 n 行
- 句间跳转
  - ) 下一句
  - ( 前一句
- 段间跳转
  - } 下一段落
  - {  }
- 其他跳转
  - g; 跳到上一次修改的地方
  - L 光标跳到屏幕下方
  - ctrl-O 执行后退
  - ctrl-I 执行前进
  - :n 命令模式跳转到第 n 行
  - %  匹配括号
  - `*` 和 # 匹配光标所在的单词，`*` 移到上一个匹配的单词处，# 移动到下一个单词处
  - gj, gk 在软换行的情况下在行中上下移动光标

## 滚动窗口

- ctrl-d 窗口向下滚动半屏
- ctrl-u 窗口向上滚动半屏
- ctrl-e 窗口向下滚动一行
- ctrl-y 窗口向上滚动一行
- ctrl-b 窗口向上滚动一页
- ctrl-f 窗口向下滚动一页
- zz     当前行位于屏幕窗口中间
- zt     当前行位于屏幕窗口顶部
- zb     当前行位于屏幕窗口底部

## 操作多窗口

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

## vim 设置

- 开启粘贴模式：set paste     // 粘贴的代码缩进和注释不会乱
- 关闭粘贴模式：set nopaste
- 显示行号：set number
- 关闭自动缩进：set noai      // set no auto indent
- 关闭智能缩进: set nosi      // set no smart indent
- 开启相对行号：set relativenumber

  优势如下：
  - 高效。如果代码比较长，比如当前的光标在 700 行处，因为跳转都是局部和小范围内的跳转，也就是在一个屏幕窗口的可是范围内跳转。使用绝对行号跳转是 705G，而使用相对行号就是 5j，可见敲击按键的次数少一些。
  - 代码块操作。对一块连续的代码块进行复制或者缩进，等操作时，块的起始位置到终止位置光标的移动用相对行号会非常方便。跟上面的类似，例如：700 行处，V 整行选中作为代码块的起始行，705G作为代码块的终止行，这是绝对行号操作方式。而相对行号，V，5j，显然按键次数更少一些。

- 开启代码折叠：set fdm = method，下面是六种折叠方式
 - manual  手工定义折叠
 - indent  缩进代表折叠
 - expr    表达式代表折叠
 - syntax  语法高亮来定义折叠
 - diff    没有变更的文本进行折叠
 - marker  文中的标示折叠

## 折叠代码

前提是开启代码折叠，下列按键才起作用。

- zc  折叠当前代码
- zo  打开当前折叠
- zm  关闭所有折叠
- zr  打开所有折叠

## 执行命令

- :!command
- :!bash  创新启动一个 bash 执行命令，而没有退出 vim，执行完命令后 exit 回到 vim
- :r !command  将命令运行的结果插入到当前行的下一行
- :n,m !command 起始行号 n 到结束行号 m 之间的内容，用 command 来处理。例如：:2,4 !sort

## 复制和移动

- yy 复制一行

## 查找替换

普通查找替换

- :s/old/new 替换行中首次出现的 old 为 new
- :s/old/new/g 替换行中所有 old 为 new
- :n,m s/old/new/g 用 new 替换 从 n 行到 m 行中的所有 old
- :%s/old/new/g 全文查找 old 替换成 new
- g 后跟 c 进行替换前的确认

批量查找替换

- 打开若干个文件，例如：`vi *.html`
- 查看当前打开的文件：`:args`
- 在所有打开的文件中批量查找替换：`argdo %s/old/new/g`
- 退出 vim
- 验证是否修改正确，用命令：`git diff`

## 多文件操作

- `vi *.js` 同时打开多个文件
- `:ls` 查看文件缓存
- `:b num` 切换到某个缓存编号

## 常用命令

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

## 操作 i 和 a 区域对象

- i 代表 in
- a 代表 around
- 语法：`<动作>i/a<对象范围>`
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

## 操作块

操作流程如下：
- ctrl-v 块的起始位置
- 向上或向下移动光标
- I 大写字母 I，代表插入操作
- 或者行尾操作，$，A，内容
- 插入的内容，如：空格或前导符 -
- ESC 退出插入操作，块的位置都会插入

## 缩进代码

操作流程如下：
- V 进入整行的可视操作模式
- 向上或向下移动光标
- < 或 > 进行左右缩进
- = 自动缩进，自动缩进就是把代码复制到其他的位置之后，使用自动缩进，一步把代码的缩进调整到位

## vim 插件管理工具 Vundle

- 安装 Vundle
```bash
mkdir -p ~/.vim/bundle
cd ~/.vim/bundle
git clone https://github.com/VundleVim/Vundle.vim.git
```
- 配置 .vimrc，直接从 wangding/tools 仓库中复制 .vimrc 文件，文件中已经配好了常用的插件
- 安装插件，在 vim 应用中运行 :PluginInstall

## 打造 vim IDE

基本的文章参考：http://efe.baidu.com/blog/vim-javascript-completion/

- ternjs/tern_for_vim
  - 安装 nodejs 环境
  - 在插件的目录下运行 npm install 安装 tern 插件需要的 node module 依赖
  - 在每个项目代码目录下创建 .tern-project 文件，描述项目中需要用到的模块
  - .tern-project 配置文件很关键，配置好了才能完成代码补全

- Valloric/YouCompleteMe
  - 安装：使用 Vundle 下载 YCM 插件
  - 在 YCM 文件夹下执行 install.py --tern-completer，可以打造成一个 JavaScript 开发环境
  - 在 YCM 文件夹下执行 install.py --clang-completer，**没有搞定**
  - 配置 .vimrc 的 `<leader>-gf` 跳转到定义处

- jiangmiao/auto-pairs
  - 安装之后直接可用，不用进行配置

- wincent/command-t
  - 安装 command-t
  - yum install -y ruby-devel
  - 编译 command-t，~/.vim/bundle/command-T/ruby/command-t/ruby extconf.rb && make
  - 用法普通模式下 `<leader>t` 打开 command-T 窗口，输入文件名缩小范围，ctrl-j,k 上下移动光标，回车打开文件。

- vim-syntastic/syntastic
  - 语法检查
  - 需要配置 .vimrc 插件器
  - 需要全局安装 int
  - 语法错误的代码，保存的时候会提示错误信息

- mattn/emmet-vim
  - html 和 css emmet 插件  
  - 安装方式：  
    - cd ~/.vim/bundle  
    - git clone https://github.com/mattn/emmet-vim  
    - vi ~/.vimrc，增加 `Plugin 'mattn/emmet-vim'`
    - OK，编写一个 html 文件测试一下，`html:5<c-y>,`

- heavenshell/vim-jsdoc
  - JSDoc 插件，生成符合 JSDoc 格式的函数块注释  
  - 安装方式：
    - cd ~/.vim/bundle  
    - git clone https://github.com/heavenshell/vim-jsdoc  
    - vi ~/.vimrc，增加 `Plugin 'heavenshell/vim-jsdoc'`
    - OK，编写一个 js 文件测试一下，写两个函数，一个不带入口参数，一个带两、三个入口参数，在普通模式下，将光标放到 function 行上，按 `:JsDoc` 奇迹产生了。

- vimcn/vimrdoc  
  - vim 的中文帮助文档  
  - 安装方式：
    - cd ~/.vim/bundle  
    - git clone https://github.com/vimcn/vimcdoc
    - vi ~/.vimrc，增加 `Plugin 'vimcn/vimcdoc'`  
    - OK，在 vim 界面下 `:help` 就可以看到中文帮助文档  

## coc.nvim 插件系统

- coc-html
- coc-tabnine
- coc-css
- coc-json
- coc-tsserver
- coc-emmet
- coc-pairs
- coc-sql
- coc-snippets
- honza/vim-snippets snippets 代码库，coc-snippets 配合这个库才能起作用

## 键盘映射

键盘映射是 vim 高效率的关键所在。

- 参考资料：http://www.cnblogs.com/softwaretesting/archive/2011/09/28/2194515.html

## 操作技巧

技巧一：切换前后台

- vim 打开文档，编辑，保存文件，不退出 vim
- Ctrl+Z 将 vim 至于后台，进入命令行
- 命令行可以执行任意想要的操作，例如：git 命令，提交变更，推送仓库，等
- 命令行执行 fg 回到 vim，继续编辑文档

## 杂项

l :source ~/.vimrc 不退出 vim 重新加载配置文件

## 参考资料

官方资料

- [官网](http://www.vim.org/)
- [插件](http://www.vim.org/scripts/script_search_results.php?order_by=rating)
- [中文帮助文档](https://vimcn.github.io/vimcdoc/doc/help.html)

文章教程

- [一起来说 vim 语](http://www.jianshu.com/p/a361ce8c97bc)
- [vim 练级攻略](https://globalinheart.wordpress.com/2011/09/07/简明-vim-练级攻略/)
- [知乎 vim 专栏](https://zhuanlan.zhihu.com/hack-vim)
