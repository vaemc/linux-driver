支持RTL8188EUS、RTL8188ETV
## 加载驱动
```
insmod 8188eus.ko
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