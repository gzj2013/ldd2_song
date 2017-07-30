# globalmem 在用户空间的验证

## 1.加载内核
使用`make modules_install`安装驱动之后，可以使用`modprobe`命令进行模块的装载。

```bash
[root@itop ]# depmod
[root@itop ]# modprobe fsmod
[root@itop ]# modinfo fsmod
[root@itop ]# lsmod

[root@itop ]# cat /proc/devices
Character devices:
  1 mem
    ... 
  248 globalmem

[root@itop ]# mknod /dev/globalmem c 248 0
[root@itop ]# echo "hello world" > /dev/globalmem 
[root@itop ]# cat /dev/globalmem 
[10204.911303] read 4096 bytes(s) from 0 
hello world 

[root@itop ]# ls /sys/module/globalmem/
```


## 卸载内核

```bash
[root@itop ]# rmmod fsmod
```
