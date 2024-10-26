支持RTL8188EUS、RTL8188ETV

# 使用方法
将milkv duo的usb改成usb-host模式
```
ln -sf /mnt/system/usb-host.sh /mnt/system/usb.sh
sync
reboot
```

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
