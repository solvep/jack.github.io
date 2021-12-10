\---

layout:   post

title:    "Rockchip GPIO函数调用，控制LED"

subtitle:  ""

date:    2021-12-10 21:00:00

author:   "Jack"

catalog: false

header-style: text

tags:

 \- Linux

\---

Rockchip GPIO函数调用，控制LED

看原理图，找到控制GPIO的引脚

GPIO常用系统调用函数：

位于include/linux/gpio.h

1. 申请GPIO

   `static inline int gpio_request(unsigned gpio,const char *label)`

2. 设置GPIO电平

   `static inline void gpio_set_value(unsigned int gpio)`

3. 获取GPIO电平

   `static inline int gpio_get_output(unsigned gpio)`

4. 设置GPIO为输出，并设置电平

   `static inline int gpio_direction_output(unsigned gpio, int value)`

5. 设置GPIO为输入

   `static inline int gpio_direction_input(unsigned gpio)`



show code 

`#include <linux/kernel.h>`

`#include <linux/init.h>`

`#include <linux/module.h>`

`#include <linux/delay.h>// mdelay()方法 用于延时`

`#include <linux/gpio.h> // 包含上面介绍的操作GPIO的方法`

`#define LED_GPIO 258 // 258 怎么来的，在原理图上找到LED的控制引脚`

`GPIO8_A2  该设备对应设备树的编号是258？`

`#define GPIO_LOW 0`

`#define GPIO_HIGH 1`

`static viod mos_short (viod) {`

​	`gpio_set_value(LED_GPIO, GPIO_LOW);`

​	`mdelay(500);`

`gpio_set_value(LED_GPIO,GPIO_HIGH);`

`mdelay(500);`

`printk("mos short\n");`

`}`

`static viod mos_long (viod) {`

​	`gpio_set_value(LED_GPIO, GPIO_LOW);`

​	`mdelay(1000);`

`gpio_set_value(LED_GPIO,GPIO_HIGH);`

`mdelay(1000);`

`printk("mos short\n");`

`}`

`static int __init hell0_init(void) {`

​	`int i;`

​	`for(i=0; i<=10;i++) {`

​	`printk("----------hello word-----------");`

`gpio_set_value(LED_GPIO, GPIO_LOW);`

`printk("the led lever is : %d\n", gpio_get_value(LED_GPIO));`

​	`mdelay(500);`

`gpio_set_value(LED_GPIO,GPIO_HIGH);`

`mdelay(500);`

`}`

`}`

`static viod __exit hello_exit(void){`

`printk("Exit hello world\n")`

`}`

`subsys_inicall(hello_init)`

`module_exit(hello_exit)`



`MODULE_AUTHOR("Jack <>")`

`MODULE_DESCRIPTION("YDT")`

`MODULE_LICENSE("GPL")`



