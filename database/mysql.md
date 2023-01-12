# MySQL

## MySQL Shell 快捷键

常用的快捷键整理如下，不常用的不收录

```
Standard key bindings

"^A"           ->  ed-move-to-beg         # 光标移到行首
"^E"           ->  ed-move-to-end         # 光标移到行尾

"^B"           ->  ed-prev-char           # 光标左移一个字符
"^F"           ->  ed-next-char           # 光标右移一个字符

"^C"           ->  ed-ignore              # 取消编辑

"^D"           ->  em-delete-or-list      # 删除光标右侧一个字符
"^H"           ->  em-delete-prev-char    # 删除光标左侧一个字符

"^K"           ->  ed-kill-line           # 删除光标右侧到行尾
"^W"           ->  em-kill-region         # 删除光标左侧到行首

"^L"           ->  ed-clear-screen        # 清除屏幕内容

"^P"           ->  ed-prev-history        # 向前调出历史命令
"^N"           ->  ed-next-history        # 向后调出历史命令

"^R"           ->  em-inc-search-prev     # 增量搜索历史命令

"^T"           ->  ed-transpose-chars     # 交换光标和光标前一个字符

"^U"           ->  em-kill-line           # 删除一行

Alternative key bindings or Multi-character bindings

"^[D"          ->  em-delete-next-word   # 删除光标右侧的一个单词
"^[^H"         ->  em-delete-next-word   # 删除光标左侧的一个单词

"^[U"          ->  em-upper-case         # 将光标右侧的一个单词转为大写
"^[L"          ->  em-lower-case         # 将光标右侧的一个单词转为小写

"^[b"          ->  ed-prev-word          # 光标左移一个单词
"^[f"          ->  em-next-word          # 光标右移一个单词
```

**注释：**

- `tab` 键用来代码补全
- `->` 左侧是快捷键，右侧是该快捷键的功能描述
- 快捷键分两大类，第一类："^A" ~ "^U"，第二类："^[D" ~ "^[f"
- 双引号中的内容是快捷键，快捷键不包含双引号
- "^A" 是 `Ctrl + A`，下面类似，注意 `A` 键不需要大写
- "^[D" 是 `Alt + D` 或者 `Ctrl + [ + D`，下面类似
- 前缀说明，`ed` 代表 `line editor`，`em` 代表 `emacs mode`，`rl` 代表 `read line`

## 修改数据库密码强度（v5.7）

- SHOW VARIABLES LIKE 'validate_password%';
- set global validate_password_policy=0;
- set global validate_password_length=3;

