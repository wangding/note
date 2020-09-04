# win10 操作系统

## 文件夹共享问题

一个 win10 电脑访问，另一个 win10 电脑上的共享文件夹。设了网络驱动器 z 盘，刚开始能访问，后来不能访问了。提示：本地设备名已在使用中。此连接尚未还原。

解决办法：
- cmd 进入命令行
- `net use * /delete` 删除所有映射的盘符
- win + r，打开运行对话框，输入 UNC 路径，例如：`\\wd-pc`
- 在资源管理器中，创新映射网络盘符

## 解决了弹窗的问题

https://www.zhihu.com/question/24265718

## 小娜不工作
小娜不能启动应用程序的处理办法
http://www.xitongcheng.cc/xtjc/12276.html
系统管理员身份打开 powershell
运行下面的命令，重新注册启动小娜
Get-AppXPackage -Name Microsoft.Windows.Cortana | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}

## 小娜启动绿色软件

小娜启动绿色软件的步骤
- 在开始菜单中创建快捷键
- 没有权限，首先设置权限
- 添加了快捷方式后，小娜就能正常工作了

## win10 磁盘占用百分之百

- http://jingyan.baidu.com/article/2f9b480d94898541cb6cc282.html

## 阻止 win10 自动安装软件

http://jingyan.baidu.com/article/4dc40848b152cdc8d846f143.html
