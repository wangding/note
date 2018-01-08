# ESLint

## 简介

略

## 安装 

```bash
npm i -g eslint eslint-config-airbnb eslint-plugin-import
```

## 使用

命令行静态代码检查

```bash
eslint *.js
cd nodejs-demo
find . | grep "^\.\/[0-9]\{2\}.*js$" | xargs eslint
```

vim 集成，编辑 .vimrc 文件

```
let g:syntastic_javascript_checkers=['eslint']
```

## ESLint 配置

ESLint 配置有两种主要方法：
- 注释配置，使用 JavaScript 注释将配置信息直接嵌入代码文件中
- 文件配置，使用 JavaScript、JSON 或 YAML 文件指定整个目录及其所有子目录的配置信息
可以是 package.json 文件中的 `.eslintrc.*` 文件或 eslintConfig 字段的形式，这两个 ESLint 都将自动查找和读取，也可以在命令行中指定配置文件。






【参考资料】
- ESLint 官网：https://eslint.cn/
- ESLint 使用入门：https://csspod.com/getting-started-with-eslint/
- https://segmentfault.com/t/eslint/blogs
- JavaScript 代码检查工具对比：https://segmentfault.com/a/1190000010264410


