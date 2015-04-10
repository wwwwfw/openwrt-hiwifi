# 极路由HC6361 OpenWrt固件补丁 (HiWiFi tw150v1) #

## 说明 ##
  * OpenWrt官方源码自r40975起（2014/06/02）支持HC6361，本项目只做基于官方版本的优化。
  * OpenWrt HC6361 Wiki: http://wiki.openwrt.org/toh/hiwifi/hc6361
  * 【旧版】编译方法、固件下载请移步至：https://code.google.com/p/openwrt-hiwifi/wiki/ProjectIntroduction

## HC6361 OpenWrt固件生成方法 ##
  * 下载源代码，并配置
```
svn co svn://svn.openwrt.org/openwrt/trunk openwrt-ar71xx
cd openwrt-ar71xx
make menuconfig
```
  * 在“make menuconfig”中，做如下设置
```
Target System: Atheros AR7xxx/AR9xxx
Subtarget: Generic
Target Profile: !HiWiFi HC6361
```
  * 然后按ESC保存配置退出
  * 编译
```
make V=s -jN   # N=编译机CPU数目
```
> 注意处理好编译错误，大部分错误是由于源码包无法下载，请Google搜索文件名手动下载一个放到 dl 目录即可。
  * squashfs格式固件，请使用sysupgrade命令刷入
```
openwrt-ar71xx-generic-hiwifi-hc6361-squashfs-sysupgrade.bin
```
  * 极路由“recovery.bin”格式固件生成方法
> > 需要注意的是，OpenWrt官方代码只生成了sysupgrade格式的固件，某些老版本u-boot的极1可能无法直接通过tftp刷机。处理方法很简单，就是在sysupgrade文件之前增加128KB的u-boot前缀即可。具体请参考以下方法（生成方法在Makefile里）：
```
svn co https://openwrt-hiwifi.googlecode.com/svn/branches/hiwifi-hc6361-tools/tw150v1
cd tw150v1
make
```

## 初始配置优化 ##
  * 复制以下命令，粘贴到路由器的命令行，运行成功后重启：
```
# LED settings
uci batch <<EOF
set system.led_sys='led'
set system.led_sys.name='system'
set system.led_sys.default='1'
set system.led_sys.sysfs='hiwifi:blue:system'
set system.led_sys.trigger='timer'
set system.led_sys.delayon='1000'
set system.led_sys.delayoff='1000'

set system.led_inet='led'
set system.led_inet.name='internet'
set system.led_inet.default='0'
set system.led_inet.sysfs='hiwifi:blue:internet'
set system.led_inet.trigger='netdev'
set system.led_inet.dev='eth1'
set system.led_inet.mode='link tx rx'

set system.led_wlan='led'
set system.led_wlan.name='wireless'
set system.led_wlan.default='0'
set system.led_wlan.sysfs='hiwifi:blue:wlan-2p4'
set system.led_wlan.trigger='phy0tpt'
EOF
uci commit

# Install luci
opkg update
opkg install luci
/etc/init.d/uhttpd enable
/etc/init.d/uhttpd start

```


---


# OpenWrt Firmware Patch for HiWiFi HC6361 (tw150v1) #