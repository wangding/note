# GitBook

GitBook 的安装配置，以及一些插件信息，当前使用的 GitBook 版本为 3.2.3。

## 常用命令

- 安装 GitBook 命令行工具

```bash
npm i -g gitbook-cli
```

- 其他命令

```bash
# 安装 GitBook 插件
gitbook install

# 生成 GitBook 静态网站
gitbook build

# 构建 Gitbook，并在 8080 端口上，运行 GitBook 网站
# md 文件有更新后，会自动重新构建
gitbook serve --port 8080
```

## 参考资料

- [gitbook 官方文档（中文）](https://snowdreams1006.github.io/gitbook-official/zh/)
- [梦之雪技术驿站](https://snowdreams1006.github.io)，GitBook 插件数量介绍的不多，但是每个插件的效果介绍的很详细。最重要的是详细介绍了 GitTalk 评论插件的用法
- [gitbook-use](https://github.com/zhangjikai/gitbook-use)，对 GitBook 介绍的非常全面，插件介绍的很多很全
- [刘士电子书综合插件](https://github.com/liushilive/gitbook-plugin-books)，刘士做的综合插件，图片弹出层效果不错，页脚的页面访问计数效果不错，缺点是对源插件的样式改动太大
- [gitbook](http://www.chengweiyang.cn/gitbook/)
- [gitbook 插件整理](https://www.jianshu.com/p/427b8bb066e6)
