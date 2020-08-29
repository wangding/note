# cVim

chrome 的 cVim 插件。

## 修改默认搜索引擎

cVim 插件将 Google 搜索作为默认的搜索引擎，下面介绍如何修改 cVim 插件的默认搜素引擎，以改为百度搜索引擎为例：
1. 输入 :settings，按下回车，打开 cVim 插件的设置界面
2. 输入下列代码，并保存

```javascript
let searchengine baidu = "https://www.baidu.com/s?wd=%s"
let searchengine baidu = ["https://www.baidu.com", "https://www.baidu.com/s?wd=%s"]
let completionengines = ["baidu"]
let defaultengine = "baidu"
```

## cVim link hints 模式失效的解决办法

- 找到 chrome 插件的安装路径
- 在 chrome 地址栏中输入，`chrome://version/`
- 在页面中找到个人资料路径
- 在资源管理器中，打开个人资料路径下的 Extensions 目录
- 查找 hints.js 代码文件
- 编辑 727 行，把代码 `main.createShadowRoot()` 替换成 `main.attachShadow(mode: {'open'})`
- 在 chrome 地址栏中输入：`chrome://extensions/`
- 打开开发者模式，加载已解压的扩展程序，找到 cVim 扩展程序的目录
- chrome 重新加载 cVim 插件，问题就解决了

## cVim 控制台报错

- 问题描述：https://github.com/1995eaton/chromium-vim/issues/680
- 解决办法：
- 修改 cVim 插件的 `messenger.js ` 代码文件
- 在 `port.onMessage.addListener` 函数后加 `return true;`
- 在 `chrome.extension.onMessage.addListener` 函数后加 `return true`
- 重新加载 cVim 插件

## 参考资料

- [cVim 快捷键表](https://github.com/acehjm/cVim-help)
