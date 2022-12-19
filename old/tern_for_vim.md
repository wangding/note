# tern_for_vim

tern_for_vim 插件的用法。

## 官方文档资料

- http://ternjs.net/doc/manual.html#plugin_commonjs

## 配置的例子

.tern-project 配置文件的内容。

- 下面的例子是做 nodejs 后端开发的案例。支持 CommonJS module 插件的代码补全。

```javascript
{
  "libs": [
    "browser",
    "jquery"
    ],
  "plugins": {
    "node": {},
    "modules": {
      "modules": "./node_modules/selenium-webdriver/index.js"
    }
  }
}
```

- 下面的例子是做前端开发的案例。

```javascript
{
  "libs": [
      "browser",
      "jquery"
    ],
    "loadEagerly": [
    "importantfile.js"
      ],
    "plugins": {
      "requirejs": {
        "baseURL": "./",
        "paths": {}
      }
    }
}
```
