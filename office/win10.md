# 解决了弹窗的问题
https://www.zhihu.com/question/24265718

# 去掉六个文件夹
原文地址：
http://www.askvg.com/tip-remove-6-extra-folders-from-windows-10-explorer-this-pc/

主要内容摘录如下：

![6 Extra Folders](http://media.askvg.com/articles/images5/Extra_Folders_Windows_10_This_PC.png)

Now in Windows 10, Microsoft is using a new string "**ThisPCPolicy**" in Registry to show or hide items in "This PC" window. If the string value is set to "**Show**", that particular item is shown in "This PC" window and if the string value is set to "**Hide**", that item is not shown in "This PC" window.
So we just need to change the value of "**ThisPCPolicy**" to "**Hide**" for all 6 folders CLSID in Registry and they will immediately disappear from "This PC" window.
If you also want to remove those extra and annoying 6 folders from Windows 10 "This PC" window, check out following simple steps:
**1.** Press **WIN+R** keys together to open RUN dialog box. You can also open it from WIN+X menu. Now type **regedit** in RUN dialog box and press Enter. It'll open **Registry Editor**.
**2.** Now go to following keys one by one:
**For Pictures folder:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ FolderDescriptions\{0ddd015d-b06c-45d5-8c4c-f59713854639}\PropertyBag
**For Videos folder:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ FolderDescriptions\{35286a68-3c57-41a1-bbb1-0eae73d76c95}\PropertyBag
**For Downloads folder:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ FolderDescriptions\{7d83ee9b-2244-4e70-b1f5-5393042af1e4}\PropertyBag
**For Music folder:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ FolderDescriptions\{a0c69a99-21c8-4671-8703-7934162fcf1d}\PropertyBag
**For Desktop folder:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ FolderDescriptions\{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}\PropertyBag
**For Documents folder:**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\ FolderDescriptions\{f42ee2d3-909f-4907-8871-4c22fc0bf756}\PropertyBag

![Desktop](http://media.askvg.com/articles/images5/Hide_This_PC_Folders_Windows_10_Registry.png)

**NOTE:** All above mentioned keys contain "**ThisPCPolicy**" string except "**{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}**" key which isresponsible
(负责的)
for **Desktop** folder. So you'll need tomanually
(手动地)
create new string "**ThisPCPolicy**" and set its value to **Hide** for this key.
**3.** That's it. Now open "This PC" window and you'll no longer see those extra 6 folders.

![Removed](http://media.askvg.com/articles/images5/No_Extra_Folders_Windows_10_This_PC.png)

经验证有效。

# 小娜不工作
小娜不能启动应用程序的处理办法
http://www.xitongcheng.cc/xtjc/12276.html
系统管理员身份打开 powershell
运行下面的命令，重新注册启动小娜
Get-AppXPackage -Name Microsoft.Windows.Cortana | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}

# 小娜启动绿色软件
小娜启动绿色软件的步骤
- 在开始菜单中创建快捷键
- 没有权限，首先设置权限
- 添加了快捷方式后，小娜就能正常工作了