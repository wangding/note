# npm 用法

51CTO 学院有 npm 包管理的一门课程，九元讲的还行，可能没有阮一峰讲的深入。

## 参考资料

- 阮一峰：npm 模块安装机制简介  
  http://www.ruanyifeng.com/blog/2016/01/npm-install.html  
- 阮一峰：JavaScript 教程的 NodeJS 章节中的部分内容  
  http://javascript.ruanyifeng.com/nodejs/packagejson.html  
- 阮一峰：npm scripts 使用指南  
  http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html  
- 阮一峰：package.json 详解  
  http://javascript.ruanyifeng.com/nodejs/packagejson.html  
- npm help install  
- npm 命令的用法：
  http://blog.sina.com.cn/s/blog_4a2defca0102w6c0.html
- 常用的命令：
  - npm install  
  - npm install express --registry=https://registry.npm.taobao.org 这个方式不好用，直接 npm install express 就行
  - npm init  
  - npm login  
  - npm logout  
- how-to-npm 教程  

## 重要知识点

- npm 是什么？  
  - npm 是 node package management 的缩写。npm 是一个 node 包管理和分发工具，已经成为了非官方的发布 node 模块（包）的标准。有了 npm，可以很快的找到特定服务要使用的包，进行下载、安装以及管理已经安装的包。

- npm 的官方网站  
  - https://www.npmjs.com/  
  
- npm install 命令的 -g 参数  
  - node 模块或应用的安装分为全局模式和本地模式。一般情况下会以本地模式运行，包会被安装到和你的应用程序代码的本地 node_modules 目录下。在全局模式下，Node 包会被安装到 Node 的安装目录下的node_modules下。
  - -g 是全局安装命令，获知使用$npm set global=true来设定安装模式，$npm get global 可以查看当前使用的安装模式。
  - 但是代码中，直接通过require()的方式是没有办法调用全局安装包的。全局的安装是供命令行使用的，就好像全局安装了 vmarket 后，就可以在命令行中直接运行 vm 命令。
  
- npm install 命令的 --save 参数或者 -S 参数  
  - 将信息写入 package.json 中项目路径中如果有 package.json 文件时，直接使用 npm install 方法就可以根据 dependencies 配置安装所有的依赖包，这样代码提交到 github 时，就不用提交 node_modules 这个文件夹了。  

- npm config get cache 查看缓存目录  
- npm cache list  查看缓存
- npm init 初始化一个 package  
- npm adduser  
- npm login  
- npm init --scope=<username>  
- npm ls 查看安装的所有包  
  - 可能会报错：extraneous 错误，需要修改 package.json 文件的 dependence  
- npm install  
  有了 package.json 文件，尤其是其中的 dependencies 字段指明了包的依赖关系后，直接使用 npm install 命令，就会在当前目录中安装所需要的模块。所以代码上传 Github 时，不用上传 node\_modules 中的内容，服务器部署的时候可以自动安装依赖包。可以做个实验把 node_modules 文件夹都删除，执行 npm install 命令看看效果。  
- npm test  
- npm publish  
- npm config set registry  
- https://www.npmjs.com/ npm 官网搜索发布的包  
- npm init & npm install <published package> & 检查 node_modules 文件夹下的东西  
- npm view  查看 package 在 npm 官网的注册参数信息，每次 publish 之后信息都会改变，不 publish 改变的本地的信息，npm view 看到的信息不变  
- npm version <new version> 设置 package 的新版本号  
- npm dist-tag 修改模块发布的标签  
- npm outdated  检查版本过期的包  
- npm update --save 更新 package.json 依赖项中的软件包  
- npm uninstall --save 删除依赖的包  
- npm unpublish <package> --force  
- npm list -g 查看全局安装的包  
