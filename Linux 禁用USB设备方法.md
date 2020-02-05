# Linux 禁用USB设备方法

还可以禁用USB设备来达到安全的目的：

```
vim /etc/modprobe.d/stopusb install usb-storage /bin/true 
```

或者使用下面的命令将USB的驱动程序删除

```
[root@rs-server ~]# mv /lib/modules/3.10.0-693.el7.x86_64/kernel/drivers/usb/storage/usb-storage.ko.xz 
```

