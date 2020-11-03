# 各种 web 技术

## jQuery 全屏滚动插件 fullPage.js

- 示例：http://www.dowebok.com/demo/2014/77/index11.html
- CDN：http://staticfile.org/
- 图片 Demo，见 demo-code 仓库 slide 目录
- 应用：可以搞教学板书图片的轮播

## 响应式网页设计

- Responsive Web Design 响应式网页设计，自适应网页设计
- 阮一峰的文章：http://www.ruanyifeng.com/blog/2012/05/responsive_web_design.html  
- 实现要点如下：
- 媒体查询 @media：https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Media_queries  
- 视口属性 viewpoint：https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag  
- 不使用绝对宽度，使用百分比宽度  
- 字体大小不用绝对值，使用相对大小 em，rem  
- 使用浮动布局 float: right|left  
- 媒体查询，选择性加载 CSS 文件  
- 图片自适应  

## SEO

- Search Engine Optimization, SEO 搜索引擎优化  
- 各种搜索引擎爬虫 User Agent：https://www.cnblogs.com/psunny/archive/2010/05/29/1746866.html  
- Chrome 浏览器修改 User Agent 方法：  
  - F12 打开开发者工具  
  - 点击开发者工具右上角的三个小点  
  - 在下拉菜单中点击 More Tools  
  - 在 More Tools 菜单中点击 Network conditions  
  - User agent 的 Select automatically 勾选去掉  
  - 在下拉列表中选择 User agent，可以是 Google 搜索引擎爬虫的 UA  
  - 也可以自定义 UA 字符串  

## favicon.ico 网站图标

- 作用价值：https://baike.baidu.com/item/favicon.ico/8944811?fr=aladdin
- 制作方法，如下：
  - 搜索并下载样图，样图最好简洁、明快  
  - 编辑样图，去掉图中的多于元素，保证图片长度和宽度像素相等，并保存  
  - 图片去背景，把图片变成背景透明图片，可以用在线抠图网站：http://www.aigei.com/bgremover/
  - 把去背景后的图片变成图标，用在线图标生成网站：http://www.faviconico.org/  
  - 可以选择 128\*128 尺寸的图标，因为一般浏览器会缓存  
  - 案例：http://sample.wangding.co/ 图标是 S 形状，代表 sample 的意思。

## 参考资料

- 网站开发人员应该知道的61件事：http://www.ruanyifeng.com/blog/2010/11/61_things_every_web_developer_should_know.html  
- Best Practices for Speeding Up Your Web Site：https://developer.yahoo.com/performance/rules.html#gzip  
- 前端开发者的基本要求：http://www.cnblogs.com/chyingp/archive/2013/04/25/a-baseline-for-front-end-developers.html

