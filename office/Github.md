Git 仓库的版本控制，好处是所有代码发展的历史都会记录下来。我们只要去看代码的每个版本，就可以从中学习到很多东西，知道代码怎么写，知道文档该怎么写。可以举例说明，比如不知道到 MarkDown 中的 TaskList  

## 学习资料

- 常用 Git 命令清单  
  http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html  
- Git 命令中文版  
  http://www.open-open.com/lib/view/open1401433488824.html  
- github 资料  
  http://www.ui.cn/detail/20957.html  
- git-it 课程资料  
  http://jlord.us/git-it/index-zhtw.html  
- git 心法（张文细）  
  https://blog.alphacamp.co/2015/01/13/git/  
- 张文细的所有 Git 资料（带视频，讲的很到位）  
  https://ihower.tw/git/  
- git ready  
  http://gitready.com/


## 资源

- 勋章：http://shields.io/  
- 进度：https://github.com/fehmicansaglam/progressed.io  

## 常见问题

- git 存储凭证  
  http://www.cnblogs.com/volnet/p/git-credentials.html
  $ git config --global credential.helper wincred
  这一行命令搞定，参考网址：https://help.github.com/articles/caching-your-github-password-in-git/

- git 撤销远程仓库的提交  
  http://www.cnblogs.com/chucklu/p/4661149.html

- Git 文件换行问题  
  http://www.cnblogs.com/flying_bat/archive/2013/09/16/3324769.html  

- 如何在 Github 的 pull request 中进行 code review
  参考：
  https://github.com/wangding/Sample/pull/1
  https://github.com/wangding/seIDE/pull/6
  https://github.com/wangding/seIDE/pull/11

- issue 过滤

  ![issue filter.png](http://upload-images.jianshu.io/upload_images/3058932-fbc953aaadb6cdf0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## Git 命令行配置

- 自动记忆凭证  
- 设置快捷键  
- 设置换行检查  

## Git 常用命令

- git stash 相关操作  

    ```bash
    # 保存进度
    git stash

    # 弹出进度
    git stash pop

    # 查看 stash 列表
    git stash list

    # 删除所有进度
    git stash clear
    ```

- git 其他操作  

    ```bash
    # 查看某个文件的提交记录
    git log <file name>

    # 把 upstream 代表的远程仓库的 master 分支拽到本地
    git pull upstream master

    # 撤销上一个 commit，前提是没有 push 到远程仓库
    git add <something>
    git commit --amend -m "some comment"
    ```
