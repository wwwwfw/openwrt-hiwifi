# 【旧版】极路由HC6361 OpenWrt固件补丁 (HiWiFi tw150v1) #

## 文件下载 ##
  * 编译日期：2014/06/22
  * 固件下载：https://docs.google.com/file/d/0B4OfGJNugH2EeHVPZ2g5VVdlSmM
  * 刷机用的TFTP服务端工具：https://openwrt-hiwifi.googlecode.com/svn/downloads/tftpd64.400-original.zip
  * 固件内置功能概述：
    * 使用OpenWrt官方代码r38140；
    * Linux 3.10.12 内核；
    * 默认启用3个LED灯的闪烁配置；
    * 支持基于VLAN的WAN口/LAN口配置；
    * 稳定版的无线驱动；
    * 支持使用sysupgrade命令升级固件；
    * 内置软件包：6relayd, relayd, radvd, IPv6 tunnel, Multi-WAN, Samba, PPTP, ...

## 关于极路由 ##
> 北京极科极客科技有限公司，发布了一款基于OpenWrt的路由器--极路由（HiWiFi）。这被认为是全球第一款智能路由器，有着良好的外观和硬件设计，非常适合运行OpenWrt。
  * 硬件配置如下:
    * Atheros AR9331 SOC
    * 64MB RAM
    * 16M Flash
    * 8GB 板载USB存储
  * 官方网址: http://www.hiwifi.com/

## 关于本项目 ##
> 本项目利用OpenWrt官方的源码编译生成兼容“极路由”的OpenWrt固件。提供了适配“极路由”的mach代码, 和用于自动生成固件的脚本。

## 系统要求 ##
  * 建议使用 Ubuntu 12.04, 其它版本Ubuntu亦可, 但未测试过.
  * 确保您的有不受限的互联网连接.

## 生成步骤 ##
  1. 下载本源码:
```
svn co https://openwrt-hiwifi.googlecode.com/svn/branches/hiwifi-v1-r38140
```
  1. 编译生成:
```
cd openwrt-hiwifi
make
```
  1. 最终 HiWiFi recovery.bin 格式的映像: **openwrt-tw150v1-recovery.bin**

## 刷机方法 ##
  1. 为你电脑的“本地连接”加一个IP: 192.168.1.88 / 255.255.255.0
  1. 解压刷机工具包（例如 tftpd64.400.rar）, 根据操作系统位数, 32位运行tftpd32, 64位运行tftpd64.
  1. 用上面生成的 openwrt-tw150v1-recovery.bin 替换刷机包目录下的 recovery.bin .
  1. 拔掉HiWiFi电源线.
  1. 网线一头连HiWiFi的LAN口, 一头连电脑.
  1. 用尖锐物按住HiWiFi背后的reset孔不松动, 同时给路由器接电.
  1. 直到看到tftpd出现进度条, 松开.
  1. 前面板的指示灯会轮流闪烁, 表明内部Flash正在擦写, 此时不要断电.
  1. ping 192.168.1.1, 直到ping通, 刷机过程总共3-5分钟.

## 检查结果 ##
  * 若长时间（超过5分钟）ping不通192.168.1.1, 可能固件有错误, 若无法通过串口看到启动信息, 建议刷回HiWiFi官方固件.
  * 建议焊接TTL串口以查看刷机过程. 参考: https://code.google.com/p/openwrt-hiwifi/wiki/SerialFlyWires.

## 目标系统配置 ##
  * 默认情况下，芯片LAN口的交换芯片不启用转发，造成网口之间不通。请参考此处添加switch配置: https://code.google.com/p/openwrt-hiwifi/wiki/OnboardSwitchConfig
  * LED灯配置请参考上面英文说明的图片链接.


---


# OpenWrt Firmware Patch for HiWiFi HC6361 (tw150v1) #

## Downloads ##
  * Date: 2014/06/22
  * Firmware: https://docs.google.com/file/d/0B4OfGJNugH2EeHVPZ2g5VVdlSmM
  * TFTP server tool: https://openwrt-hiwifi.googlecode.com/svn/downloads/tftpd64.400-original.zip
  * Summary of built-in features:
    * Based on OpenWrt official source code - [r38140](https://code.google.com/p/openwrt-hiwifi/source/detail?r=38140);
    * Linux 3.10.12;
    * Full LED configuration with proper default configuration;
    * Supports VLAN-based WAN/LAN ports configuration;
    * With stable wireless;
    * Supports upgrading firmware with "sysupgrade";
    * Integrates 6relayd, relayd, radvd, IPv6 tunneling, Multi-WAN, Samba, PPTP, ...

## About HiWiFi ##
> A Chinese company released their new OpenWrt based router named HiWiFi. This is a recently very popular "smart" router. It has very well-designed hardware, with good features as below and performance, and perfect for OpenWrt working with.

  * Features:
    * Atheros AR9331 SOC
    * 64MB RAM
    * 16M Flash
    * 8GB on-board USB Disk
  * Office Site: http://www.hiwifi.com/

> There is an IOS App in AppStore, which can be used to config and install plugin for the HiWiFi router: https://itunes.apple.com/cn/app/ji-lu-you/id598232355?mt=8

## About this Project ##
> This project is for building a general OpenWrt firmware from source code for HiWiFi router. I've written a mach file to support this, and a few scripts to generate the firmware.

## Requirements ##
  * Ubuntu 12.04 is recommended, while untested for other Ubuntu versions.
  * Make sure the host has Internet connection.

## Building Steps ##
  1. Checkout our scripts and source code:
```
svn co https://openwrt-hiwifi.googlecode.com/svn/branches/hiwifi-v1-r38140
```
  1. Build:
```
cd openwrt-hiwifi
make
```
  1. Target HiWiFi recovery.bin image: **openwrt-tw150v1-recovery.bin**

## Firmware Flash How-to ##
  1. Add a new IP on your PC's wired interface port: 192.168.1.88 / 255.255.255.0.
  1. Extract the attached utility package (e.g., tftpd64.400.rar), and run tftpd32 for Win32 or tftpd64 for Win64, listening on the interface you set the IP to.
  1. Replace the file 'recovery.bin' with 'openwrt-tw150v1-recovery.bin'.
  1. Unplug the router's power cable.
  1. Plug a cable from your PC to one of the router's LAN port.
  1. Hold the RST botton with a needle or other sharp thing, and plug the power cable.
  1. Keep holding the button until you see the 'tftpd' server shows a client is connected.
  1. Seeing the LEDs twinkling in rotation indicates the firmware is being flashed. DO NOT turn off the power until it finishes.
  1. Ping 192.168.1.1 until it echoes (will take up 3-5 mins to complete).

## Check the Results ##
  * If cannot ping 192.168.1.1 for more than 5 mins, most probably the firmware is bad, please flash to HiWiFi's official firmware if you are unable to get serial console output.
  * I strongly recommend you to deploy a TTL console for watching the flashing progress. Please refer to https://code.google.com/p/openwrt-hiwifi/wiki/SerialFlyWires

## Target System Configuration ##
  * By default, the internal switch does not forward data between wired ports. Please refer to this to add an initial "switch" configuration: https://code.google.com/p/openwrt-hiwifi/wiki/OnboardSwitchConfig
  * For LED lights configuration, please refer to the picture below:

> ![https://openwrt-hiwifi.googlecode.com/svn/trunk/docs/!HiWiFi-openwrt-LED-reference.png](https://openwrt-hiwifi.googlecode.com/svn/trunk/docs/!HiWiFi-openwrt-LED-reference.png)