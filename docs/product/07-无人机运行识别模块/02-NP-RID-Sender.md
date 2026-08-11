---
title: NP-RID-Sender
description: >-
  NP-RID-Sender 广播式无人机运行识别发射器，满足 GB 46750-2025 标准，
  支持 MAVLink/DroneCAN 协议连接飞控，通过 WiFi 或蓝牙广播无人机运行状态，
  适配 Ardupilot、PX4 等主流飞控，满足无人机飞行监管需求。
---

# 无人机运行识别发射器

<style>
/* 覆盖 Material 主题的 display:inline-block，表格占满页面宽度 */
table {
  display: table !important;
  width: 100% !important;
  table-layout: fixed;
}
table th:nth-child(1),
table td:nth-child(1) {
  width: 20%;
}
table th:nth-child(2),
table td:nth-child(2) {
  width: 20%;
}
table th:nth-child(3),
table td:nth-child(3) {
  width: 30%;
}
table th:nth-child(4),
table td:nth-child(4) {
  width: 30%;
}
</style>

## 产品说明

### 简介

NP-RID-Sender是NextPilot推出的一款广播式无人机运行识别发射器，满足GB 46750-2025标准要求，可通过WiFi或蓝牙广播无人机运行状态信号，满足对无人机飞行监管需求。目前支持MAVLink、DroneCAN协议连接，支持的飞控有Ardupilot、PX4等，**如需要支持其他飞控或协议，可定制开发**。

购买途径：[首页-NextPilot-淘宝网](https://shop103678810.taobao.com/category.htm?spm=pc_detail.30350276.shop_block.dshopinfo.52f17dd6b1ptE2)

### 产品功能

- 具备与飞控通信获取无人机运行状态的功能；
- 具备WiFi信标帧广播功能；
- 具备蓝牙5广播功能；
- 具备网页查看无人机状态功能；
- 具备虚拟RID模拟功能；
- 具备参数设置功能，可通过串口调试助手连接设备后，通过参数命令快速设置所有参数！
- 具备OTA升级功能；

### 规格参数

- 支持主控芯片：ESP32-S3/ESP32-C3；
- 接口：2个串口**（含飞控串口、调试串口）**、1个USB、1个CAN；
- 支持输入协议：MAVLink、DroneCAN；
- 支持发射信号类型：WIFI广播信标帧、蓝牙5；
- 发射功率：20dBm；
- 发射协议：GB46750；

### 硬件形态

目前支持如下几款硬件：

- NP-RID-Sender-S3-GH
- NP-RID-Sender-C3-PinMini

| 硬件外观                                                     | 硬件名称                 | 说明                                                         |
| ------------------------------------------------------------ | ------------------------ | ------------------------------------------------------------ |
| ![image-20260805155713315](imgs\NP-RID-Sender-GH板子.png)    | NP-RID-Sender-S3-GH      | 主控芯片：ESP32-S3<br />具备所有功能，可直接安装至无人机<br />连接外置天线<br />调试串口为UART2 |
| ![image-20260805160816575](imgs\image-20260805160816575.png) | NP-RID-Sender-C3-PinMini | 主控芯片：ESP32-C3<br />无外置天线、只支持蓝牙不支持WiFi广播，一般用于测试使用。<br />调试串口为UART0 |

## 接口说明

### NP-RID-Sender-S3-GH

各硬件外部接口说明如下表：

| 接口  | 引脚线序                   | 备注                                                         |
| ----- | -------------------------- | ------------------------------------------------------------ |
| USB   | USB，Type-C                | 插入计算机后会发现两路USB设备，第一路为JTAG（程序下载与调试），第二路为串口转USB（UART0），需要安装串口驱动 |
| UART1 | RX: GPIO17<br />TX: GPIO18 | **飞控串口**<br />默认波特率57600<br />接插件为J6            |
| UART2 | RX: GPIO44<br />TX: GPIO43 | **调试串口**<br />用于调试、参数配置，通过USB的第二路串口访问<br />默认波特率57600<br />接插件为J4 |
| CAN   | RX: GPIO38<br />TX: GPIO47 | 直接连接飞控CAN即可                                          |

### NP-RID-Sender-C3-PinMini

各硬件外部接口说明如下表：

| 接口  | 引脚线序                   | 备注                                                      |
| ----- | -------------------------- | --------------------------------------------------------- |
| USB   | USB，Type-C                | 程序下载与调试，JTAG                                      |
| UART0 | RX: GPIO20<br />TX: GPIO21 | **调试串口**<br />用于调试、参数配置<br />默认波特率57600 |
| UART1 | RX: GPIO2<br />TX: GPIO3   | **飞控串口**<br />默认波特率57600                         |
| CAN   | RX: GPIO4<br />TX: GPIO5   | 需要外接CAN驱动器才可以使用                               |

## 快速使用

### 设置无人机基本信息

通过产品附带的USB转串口模块，通过调试线（4pin转4pin杜邦线）连接RID设备至计算机，打开串口调试助手（下载链接[JCom | 专业的实时曲线串口助手 - Jooiee](https://www.jooiee.com/cms/ruanjian/115.html)）。连接如下图：

![调试串口连接](imgs\调试串口连接.png)

打开JCom串口调试助手后，设置串口号（自动识别）、波特率（57600），点击打开。**输入对应命令后再输入一个回车**，然后点击发送按钮即可。

![参数设置](imgs\参数设置.png)

**设置唯一产品标识**

```shell
param set UAS_ID NEXTpil0tA2C4E6G8K0M2

```

这里产品标识必须是经UOM申报后的20位数字+字母的组合。

**设置实名认证ID**

```shell
param set GB_REALNAME 12340206

```

这里实名认证ID必须是8位数字组成！

**设置无人机分类**

```shell
param set GB_UA_CLASS 1

```

数字对应的无人机分类如下：

- 0：微型<0.25kg（MICRO）
- 1：轻型0.25-4kg（LIGHT）
- 2：小型4-15kg（SMALL）
- 3：中型15-150kg（MEDIUM）
- 4：大型\>150kg（LARGE）

**设置运行类别**

```shell
param set GB_OP_CATEGORY 1

```

数字对应的运行类别如下：

- 1：OPEN（开放类）
- 2：SPECIFIC（特定类）
- 3：CERTIFIED（审定类）

设置完成后，请重启RID设备。

### 连接飞控

这里以NP-RID-Sender-S3-GH与雷迅CUAV V7+飞控为例进行连接说明。

#### 通过串口连接

可以产品附带的飞控串口连接线（4pin转6pin），连接设备UART1串口至飞控TELEM2串口。接线说明如下：

| 飞控TELEM2 | RID设备UART1 |
| ---------- | ------------ |
| 5V         | 5V           |
| GND        | GND          |
| TX         | RX           |
| RX         | TX           |

连接如下图：

![连接示例1](imgs\飞控连接1.png)

> 说明：
>
> 这里连接的是TELEM1，其默认波特率为57600，如果需要连接其他飞控串口，请设置RID模块的串口波特率。例如`param set
>
> 其他类型飞控的连接方式大同小异，只要确保通过飞控提供供电、并且将串口收发交叉连接即可！

#### 通过CAN连接

可以产品附带的飞控CAN连接线（4pin转4pin），连接设备CAN至飞控CAN1即可。

### 连接网页查看状态

无人机上电后，可将无人机置为室外空旷环境，进行搜星定位。

RID上电后，自动启动WiFi热点（热点名称NP-RID-xxxxxx，密码nextpilot），通过笔记本连接热点后，打开浏览器，输入<http://192.168.4.1，即可显示设备运行状态。>

![image-20260806213805631](imgs\image-20260806213805631.png)

## 设置参数

### 说明

可通过**调试串口**灵活设置参数进而控制设备运行逻辑，如设置串口波特率、启动WiFi热点、启动打印信息，极大方便用户在使用过程中进行测试。

### 连接串口调试助手

以打开串口调试助手软件（如JCom等），将RID设备的调试串口连接至笔记本。

> 根据接口说明查找对应板子的调试串口。

### 参数命令 {#参数命令}

相关参数命令如下表所示：

| 操作                 | 命令                       | 示例                                       |
| -------------------- | -------------------------- | ------------------------------------------ |
| 查看所有参数         | param list                 | 查看所有参数：param list                   |
| 重置参数为出厂默认值 | param reset                | 重置为默认参数：param reset                |
| 查看指定参数         | `param get [name]`         | 查看数据输出串口波特率：param get CFG_BAUD |
| 设置参数             | `param set [name] [value]` |                                            |

**命令示例**

- 设置串口1波特率：param set BAUDRATE 115200
- 设置无人机唯一标识码：param set UAS_ID prodYYMMDD0123456789
- 设置实名认证：param set GB_REALNAME 08082330
- 设置无人机为小型：param set GB_UA_CLASS 1
- 恢复默认值：param reset

> **注意事项**
>
> 设置唯一产品标识码，必须输入20个字符，否则无法设置。
>
> 设置实名登记号，必须输入8个数字字符，否则无法设置。

### 参数汇总 {#参数汇总}

常用参数说明如下表：

| 参数             | 描述                  | 备注                                                         |
| ---------------- | --------------------- | ------------------------------------------------------------ |
| WIFI_SSID        | WiFi热点名            |                                                              |
| WIFI_PASSWORD    | WiFi密码              | 隐藏显示，默认nextpilot                                      |
| UAS_ID           | 无人机唯一标识        |                                                              |
| BAUDRATE         | 串口1波特率           |                                                              |
| GB_WIFI_NAN_RATE | WiFi-NAN广播频率      | 默认1次/秒                                                   |
| GB_WIFI_BCN_RATE | WiFi-Beacon广播频率   | 默认1次/秒                                                   |
| WIFI_CHANNEL     | WiFi广播频道          |                                                              |
| WIFI_POWER       | WiFi功率              |                                                              |
| GB_BLE_RATE      | 蓝牙5广播频率         | 默认1次/秒                                                   |
| GB_REALNAME      | 实名认证，身份证后8位 |                                                              |
| GB_OP_CATEGORY   | 运行类别              | 0：未声明；<br />1：开放类；<br />2：特定类；<br />3：审定类。<br />具体参见GB46750-2025 |
| GB_UA_CLASS      | 无人机分类            | 0：微型（<0.25kg）<br />1：轻型（0.25-4kg）<br />2：小型（4-15kg）<br />3：中型（15-150kg）<br />4：大型（>150kg）<br />具体参见GB46750-2025 |
| WEBSERVER_EN     | 启动/关闭网页服务器   |                                                              |
| SIM_ON           | 启动/关闭RID模拟      |                                                              |

## 高级功能

### 模拟RID

在没有连接无人机飞控设备的条件下，如果需要进行测试，可使用该产品模拟一个RID。配置步骤如下：

1. 连接串口调试助手
2. 发送配置命令：param set SIM_ON 1
3. 重启设备即可

若需要关闭RID模拟，只需要输入`param set SIM_ON 0`，然后重启设备即可。

## OTA升级

### 下载

| 板子                     | 当前固件版本 | 点击下载                                                     |
| ------------------------ | ------------ | ------------------------------------------------------------ |
| NP-RID-Sender-S3-GH      | V1.0         | [OTA升级app固件](./固件/NP-RID-Sender-S3-GH-V1.0_OTA.bin)    |
| NP-RID-Sender-C3-PinMini | V1.0         | [OTA升级app固件](./固件/NP-RID-Sender-C3-PinMini-V1.0_OTA.bin) |

### 上传固件

连接RID设备热点，打开网页[http://192.168.4.1](http://192.168.4.1)，点击选择文件，选择下载的固件后点击Update按钮即可。

![image-20260806213848443](imgs\image-20260806213848443.png)

升级后设备自动重启。
