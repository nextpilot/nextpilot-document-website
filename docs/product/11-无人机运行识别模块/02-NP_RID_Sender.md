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

### 产品功能

- 具备与飞控通信获取无人机运行状态的功能；
- 具备WiFi广播功能；
- 具备蓝牙5广播功能；
- 具备网页查看无人机状态功能；
- 具备参数设置功能，可通过串口调试助手连接设备后，通过参数命令快速设置所有参数！
- 具备OTA升级功能；

### 规格参数

- 支持主控芯片：ESP32-S3/ESP32-C3；
- 接口：2个串口**（UART0用于调试，UART1用于连接飞控）**、1个USB、1个CAN；
- 支持输入协议：MAVLink、DroneCAN；
- 支持发射信号类型：WIFI广播信标帧、蓝牙5；
- 发射功率：20dBm；
- 发射协议：GB46750；

### 硬件形态

目前支持如下两款硬件：

- ESP32-S3-Board
- ESP32-S3-Board-mini

| 硬件外观                                                     | 硬件名称            | 说明                                                         |
| ------------------------------------------------------------ | ------------------- | ------------------------------------------------------------ |
| ![image-20260805155713315](imgs\image-20260805155713315.png) | ESP32-S3-Board      | 主控芯片：ESP32-S3<br />具备所有功能，可直接安装至无人机。<br />若进行调试：可直接使用USB线连接设备与笔记本，笔记本即可访问UART0串口。 |
| ![image-20260805160816575](imgs\image-20260805160816575.png) | ESP32-S3-Board-Mini | 主控芯片：ESP32-C3<br />无外置天线、不支持WiFi，一般用于测试使用。<br />若进行调试：需要通过单独的USB转TTL线，连接设备UART0与笔记本。 |

## 接口说明

### ESP32-S3-Board

各硬件外部接口说明如下表：

| 接口  | 引脚线序                   | 备注                                                         |
| ----- | -------------------------- | ------------------------------------------------------------ |
| USB   | USB，Type-C                | 插入计算机后会发现两路USB设备，第一路为JTAG（程序下载与调试），第二路为串口转USB（UART0），需要安装串口驱动 |
| UART0 | RX: GPIO44<br />TX: GPIO43 | 用于调试、参数配置，通过USB的第二路串口访问<br />默认波特率57600 |
| UART1 | RX: GPIO17<br />TX: GPIO18 | 用于飞控链接<br />默认波特率57600                            |
| CAN   | RX: GPIO38<br />TX: GPIO47 | 需要外接CAN驱动器才可以使用                                  |

### ESP32-C3-Board-Mini

各硬件外部接口说明如下表：

| 接口  | 引脚线序                   | 备注                                    |
| ----- | -------------------------- | --------------------------------------- |
| USB   | USB，Type-C                | 程序下载与调试，JTAG                    |
| UART0 | RX: GPIO20<br />TX: GPIO21 | 用于调试、参数配置<br />默认波特率57600 |
| UART1 | RX: GPIO2<br />TX: GPIO3   | 用于飞控链接<br />默认波特率57600       |
| CAN   | RX: GPIO4<br />TX: GPIO5   | 需要外接CAN驱动器才可以使用             |



## 快速使用

### 通过串口连接飞控

这里以ESP32-S3-Board与雷迅CUAV V7+飞控为例进行连接说明。

可以产品附带的连接线，连接设备UART1串口至飞控TELEM2串口。接线说明如下：

| 飞控TELEM2 | 设备UART1  |
| ---------- | ---------- |
| 5V         | 5V         |
| GND        | GND        |
| TX         | GPIO17(RX) |
| RX         | GPIO18(TX) |

![连接示例1](imgs\连接示例1.png)

> 说明：
>
> 其他类型飞控的连接方式大同小异，只要确保通过飞控提供供电、并且将串口收发交叉连接即可！



### 连接网页查看状态

设备上电后，自动启动WiFi热点（热点名称NP-RID-xxxxxx，密码nextpilot），通过笔记本连接热点后，打开浏览器，输入http://192.168.4.1，即可显示设备运行状态。

![image-20260806213805631](imgs\image-20260806213805631.png)

## 设置参数

### 说明

可通过**UART0串口**灵活设置参数进而控制设备运行逻辑，如设置数据输出串口、启动WiFi热点、启动打印信息，极大方便用户在使用过程中进行测试。

### 连接串口调试助手

以打开串口调试助手软件（如JCom等），将串口连接至笔记本。

> **对于ESP32S3-Board**，只需要使用Type-C USB线，连接设备USB至笔记本，然后打开带有SERIAL CH343字样的串口，波特率默认57600，点击打开即可。
>
> ![image-20260806220626360](imgs\image-20260806220626360.png)
>
> 
>
> **对于ESP32-C3-Board-Mini来说**，需要使用一个USB转TTL串口线，通过交叉方式连接设备UART串口引脚（），然后将串口线插入笔记本。

### 参数配置命令

#### 参数命令 {#参数命令}

相关参数命令如下表所示：

| 操作                 | 命令                       | 示例                                       |
| -------------------- | -------------------------- | ------------------------------------------ |
| 查看所有参数         | param list                 | 查看所有参数：param list                   |
| 重置参数为出厂默认值 | param reset                | 重置为默认参数：param reset                |
| 查看指定参数         | `param get [name]`         | 查看数据输出串口波特率：param get CFG_BAUD |
| 设置参数             | `param set [name] [value]` |                                            |

#### 命令示例

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



#### 参数汇总 {#参数汇总}

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

## OTA升级

### 下载

请访问[固件下载 - NextPilot 文档中心](https://docs.nextpilot.org/product/11-无人机运行识别模块/固件下载.html)下载NP-RID-Sender相应固件。固件名为`NP-RID-Sender-XXXX_ota.bin`，对于V1.0版本，固件名为`NP-RID-Sender-V1.0_ota.bin`。

### 上传固件

链接产品热点，打开网页[http://192.168.4.1](http://192.168.4.1)，点击选择文件，选择下载的固件后点击Update按钮即可。

![image-20260806213848443](imgs\image-20260806213848443.png)

升级后设备自动重启。

