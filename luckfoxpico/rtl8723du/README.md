
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

