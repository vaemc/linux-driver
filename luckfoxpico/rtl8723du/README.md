
# 方式1


## 设备树
\luckfox-pico\sysdrv\source\kernel\arch\arm\boot\dts\rv1103g-luckfox-pico.dts
```
&gmac {
	status = "okay";
};
```

## SDK全局配置支持WiFi
\luckfox-pico\project\cfg\BoardConfig_IPC\BoardConfig-EMMC-NONE-RV1103_Luckfox_Pico-IPC.mk
```
export RK_ENABLE_WIFI=y
```

## 加载驱动
```
insmod libarc4.ko
insmod cfg80211.ko
insmod mac80211.ko
insmod 8723du.ko
```

## 开启网卡
```
ifconfig wlan0 up
wpa_supplicant -D nl80211 -i wlan0 -c /etc/wpa_supplicant.conf &
```

## 获取IP
### 动态IP
```
udhcpc -i wlan0
```

## 静态IP
```
ifconfig wlan0 192.168.5.119 netmask 255.255.255.0
route add default gw 192.168.5.1
```

# 方式2

1. 将1文件夹下的lib所有文件复制到linux系统下的/lib,
2. 执行modprobe 8723du
3. 执行reboot


