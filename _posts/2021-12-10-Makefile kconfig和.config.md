---

layout:   post

title:    "Makefile Kconfig 和 .config 的关系"

subtitle:  ""

date:    2021-12-10 21:00:00

author:   "Jack"

catalog: false

header-style: text

tags:

 - Linux

---

## Makefile Kconfig 和 .config 的关系

#### Makefile Kconfig 和.config 的关系

Kconfig：对应着内核的配置菜单

Makefile: 编译源文件的方法

.config: 编译所依据的配置



#### Kconfig 的语法

1. 一个典型的内核配置菜单

2. kconfig 的类型定义

   bool 布尔类型 选择是否编译进内核，tristate三态（内建，模块，移除）编译到内核编译成模块，string字符串，integer整型等

3. 目录层次的嵌套：在Kconfig中由类似语句：source "drivers/usb/Kconfig"

   用来包含或嵌套新的Kconfig文件，这样便可以使各个目录管理各自的配置内容，使不必把那些配置都写在同一个文件里，方便修改和管理。



#### Makefile的语法

1. 直接编译

   obj-y += gsl_point_id.o

2. 条件编译

   obj-$(CONFIG_TOUCHSCREEN_GSLX680) += rockchip_gsIX680.o

3. 编译目录

   obj-$(CONFIG_TOUCHSCREEN_SYNAPTICS_RMI4_I2C_RK) += rmi4/

#### .config

.config 的修改方式

1. 通过make menuconfig  // 图形界面的配置
2. make xxx_defcofing
3. 直接修改