# 模块被编译时会前后两次进入该目录进行编译。
# 在该目录下（即模块所在的目录）执行make命令时，第一次根据该Makefile
# 进行编译，此时KERNELRELEASE变量的值为空，所以ifeq条件成立。
# KERNELRELEASE是在内核源码树的顶层Makefile中定义的一个变量，其值为
# 内核的版本号。
ifeq ($(KERNELRELEASE),)

PWD := $(shell pwd)
# 定义内核源码所在目录的变量，该目录下的内核源码应该是被移植好的内核
# 源码，并且经过了正确的配置和编译，修改Makefile时需要修改该变量的值。
KERNELDIR ?= /home/ldd/work/gitwork/itop4412_kernel_3.0
# 定义根文件系统的目录，该目录即为NFS挂载的主机目录。模块将被安装在
# 该目录下的lib/modules/<内核版本号>/extra目录下，修改Makefile时需要
# 修改该变量的值。
INSTALLDIR ?= /home/ldd/source/nfs/rootfs

# 第一个目标，为默认的目标，即执行make modules命令和执行make命令的效果相同。
modules:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) modules

# 用于模块的安装，推荐使用该方式，这样可以使用modprobe命令进行模块的装载。
modules_install:
	$(MAKE) -C $(KERNELDIR) M=$(PWD) INSTALL_MOD_PATH=$(INSTALLDIR) modules_install
clean:
	rm -rf *.o *.ko *.mod.c .*.cmd modules.order Module.symvers .tmp_versions

else
# 第二次进入模块所在的目录进行编译时，由于KERNELRELEASE变量已被定义，

obj-m := globalmem.o

endif
