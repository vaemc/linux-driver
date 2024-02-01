# 使用方法

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

