# STM32F40x 板级支持包

## 1. 简介

STM32F40x 是由意法半导体推出的Cortex-M4内核的高性能单片机
包括如下硬件特性：

| 硬件 | 描述 |
| -- | -- |
|芯片型号| STM32F40x全系列 |
|CPU| Cortex-M4 |
|主频| 84MHz-208MHz |

## 2. 编译说明


| 环境         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| PC操作系统   | Linux/MacOS/Windows                                          |
| 编译器       | arm-none-eabi-gcc version 6.3.1 20170620 (release)/armcc/iar |
| 构建工具     | scons/mdk5/iar                                               |
| 依赖软件环境 | Env工具/(MDK或IAR或arm-none-eabi-gcc)/git/调试器驱动         |

1) 下载源码

```bash
    git clone https://github.com/RT-Thread/rt-thread.git
```

2) 配置工程并准备env

（Linux/Mac）

```bash
    cd rt-thread/bsp/stm32f40x
    scons --menuconfig
    source ~/.env/env.sh
    pkgs --upgrade
```

（Windows）

>在[RT-Thread官网][1]下载ENV工具包

3) 配置芯片型号

（Linux/Mac）

```bash
    scons --menuconfig
```

（Windows(ENV环境中)）

```bash
    menuconfig
```

在menuconfig页面配置并选择对应的芯片型号，若开发环境为MDK/IAR，则需要生成工程

4) 生成工程(Mac/Linux下请跳过此步骤)

（Windows IAR）

```bash
    SET RTT_CC=iar
    scons --target=iar -s
```

（Windows MDK5）

```bash
    scons --target=mdk5 -s
```

（Windows MDK4）

```bash
    scons --target=mdk4 -s
```

5) 编译

使用MDK或IAR请参见对应教程

（Windows arm-none-eabi-gcc）
使用以下指令设置gcc路径

```bash
    SET RTT_EXEC_PATH=[GCC路径]
```

（Linux/Mac arm-none-eabi-gcc）
使用以下指令设置gcc路径

```bash
    export RTT_EXEC_PATH=[GCC路径]
```

编译（WindowsLinux/Mac arm-none-eabi-gcc）

```bash
    scons -j4
```

出现下列信息即为编译成功

```bash
    LINK rtthread-stm32f4xx.elf
    arm-none-eabi-objcopy -O binary rtthread-stm32f4xx.elf rtthread.bin
    arm-none-eabi-size rtthread-stm32f4xx.elf
    text    data     bss     dec     hex filename
    41596     356    1456   43408    a990 rtthread-stm32f4xx.elf
    scons: done building targets.
```


如果编译正确无误，会产生rtthread-stm23f4xx.elf、rtthread.bin文件。其中rtthread.bin为二进制固件

## 3. 烧写及执行

烧写可以使用仿真器 ISP等多种方式 此处不再赘述

### 3.1 运行结果

如果编译 & 烧写无误，会在串口2*上看到RT-Thread的启动logo信息：

```bash
 \ | /
- RT -     Thread Operating System
 / | \     3.0.4 build May 15 2018
 2006 - 2018 Copyright by rt-thread team
msh />
```

*默认串口


## 4. 驱动支持情况及计划

| 驱动    | 支持情况 | 备注          |
| ------- | :------: | :-----------: |
| UART    | 支持     | UART1/2/3/4/5 |
| GPIO    | 支持     | /             |
| hwtimer | 支持     | /             |
| RTC     | 支持     | /             |
| eth     | 支持     | LAN8720A      |

### 4.1 IO在板级支持包中的映射情况

| IO号 | 板级包中的定义 |
| -- | -- |
| PB6 | USART1 TX |
| PB7 | USART1 RX |
| PA2 | USART2 TX |
| PA3 | USART2 RX |
| PD8 | USART3 TX |
| PD9 | USART3 RX |
| PC10 | UART4 TX |
| PC11 | UART4 RX |
| PC12 | UART5 TX |
| PD2 | UART5 RX |

## 5. menuconfig Bsp菜单详解

| 选项 | 解释 |
| -- | -- |
| Enable UART1 (PB6/7) | 开启串口1，串口1的设备名为"uart1" |
| Enable UART2 (PA2/3) | 开启串口2，串口1的设备名为"uart2" |
| Enable UART3 (PD8/9) | 开启串口3，串口1的设备名为"uart3" |
| Enable UART4 (PC10/11) | 开启串口4，串口1的设备名为"uart4" |
| Enable UART5 (PC12/PD2) | 开启串口5，串口1的设备名为"uart5" |

*部分选项需要在RT-Thread组件菜单中开启对应的设备框架才能显示。

## 6. 联系人信息

维护人:
[uestczyh222][4] < [lymz@foxmail.com][5] >

  [1]: https://www.rt-thread.org/page/download.html
  [4]: https://github.com/uestczyh222
  [5]: mailto:lymz@foxmail.com
