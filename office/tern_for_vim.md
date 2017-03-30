# tern_for_vim

tern_for_vim 插件的用法。

## 官方文档资料

- http://ternjs.net/doc/manual.html#plugin_commonjs

## 配置的例子

.tern-project 配置文件的内容。

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
