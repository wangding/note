# vmware 虚拟机

vmware workstation 虚拟机软件的使用。

## 快速创建虚拟机

已经有了一个虚拟机，可以在这个虚拟机的基础上快速创建另一个虚拟机。对虚拟机文件夹进行复制就行。但是，一定要注意几点：
- 复制虚拟机之前，虚拟机一定要关机，不能使挂起状态；
- 复制虚拟机后，修改网卡的 MAC 地址，避免冲突；
- 复制虚拟机后，修改网卡的 IP 地址，避免冲突；

## 快捷键操作

- Ctrl + Alt
  可以把光标从虚拟机界面中释放出来，这个时候就可以用 Ctrl + win + <- 来切换到 win10 的其他桌面了。这样就可以把虚拟机的窗口全屏。

- Ctrl + G
  Ctrl + Win + -> 把 win10 桌面切换到虚拟机的窗口时，虚拟机并没有获得焦点，这时可以用快捷键来进入虚拟机，也可以用鼠标点击虚拟机界面中的窗口，直接操作。

## 故障排除

-  安装 vmware win10 没有 vmnet8 网卡，参考[链接](https://www.jianshu.com/p/f2c7af8081e1)
- vmnet8 网卡的 IP 地址是 169.254.XXX.XXX，vmware 的 DHCP 服务没有启动
- linux 虚拟机 `ping www.baidu.com`，或者 `ping 192.168.133.2` 网关 ping 不到，可能是 vmware nat 服务没有启动
- 确保 vmware 以下五个服务程序都是启动的
  - VMware Workstation Server
  - VMware NAT Service
  - VMware USB Arbitration Service
  - VMware DHCP Service
  - VMware Authorization Service
