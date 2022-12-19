# Phantomjs

## 安装 phantomJS

http://www.cnblogs.com/LH2014/p/4073881.html

```bash
# 安装依赖软件
yum install -y wget fontconfig

# 下载安装包
wget -c https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2

# 解压缩
tar jxvf phantomjs-2.1.1-linux-x86_64.tar.bz2

如果 tar 出错，错误信息是：tar (child): bzip2：无法 exec: 没有那个文件或目录
则说明没有安装 bzip2
yum intall -y bzip2

# 移动位置
mv phantomjs-2.1.1-linux-x86_64 /usr/local/src/phantomjs

# 建立软连接
ln -sf /usr/local/src/phantomjs/bin/phantomjs /usr/local/bin/phantomjs
```

## Selenium + Phantomjs 的测试代码

貌似跑通了

```javascript
var webdriver = require('selenium-webdriver'),
    By = webdriver.By,
    until = webdriver.until;

var driver = new webdriver.Builder()
    .forBrowser('phantomjs')
    .build();

driver.get('http://www.baidu.com');
driver.findElement(By.id('kw')).sendKeys('selenium');
driver.findElement(By.id('su')).click();
driver.wait(until.titleIs('selenium_百度搜索'), 1000);
console.log('OK!');
driver.quit();
```

## 官方资料

http://phantomjs.org/quick-start.html