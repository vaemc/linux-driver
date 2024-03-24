
# 使用方法


## 设备树
\luckfox-pico\sysdrv\source\kernel\arch\arm\boot\dts\rv1103g-luckfox-pico.dts
```
&gmac {
	status = "okay";
};

&usbdrd_dwc3 {
    status = "okay";
    dr_mode = "host";
};
```

## SDK全局配置支持WiFi
\luckfox-pico\project\cfg\BoardConfig_IPC\BoardConfig-EMMC-NONE-RV1103_Luckfox_Pico-IPC.mk
```
export RK_ENABLE_WIFI=y
```

## 加载固件
复制rtl8188eufw.bin固件到/lib/firmware/rtlwifi

## 加载驱动
```
insmod 8188eu.ko
```

## 开启网卡
```
ifconfig wlan0 up
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant.conf -Dwext
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

