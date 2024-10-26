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

## 启用网卡
```
ifconfig wlan0 up
```

## 连接wifi
到wpa_supplicant.conf编辑wifi账号和密码，然后执行(只能连接2.4 GHz wifi)
```
wpa_supplicant -D nl80211 -i wlan0 -c /etc/wpa_supplicant.conf &
```

## 获取IP
### 动态IP
```
udhcpc -i wlan0
```

# 联网脚本
创建文件
```
touch wifi.sh
```

内容
```
#!/bin/bash

if [ $# -ne 3 ]; then
    echo "Usage: $0 <module_file> <wifi_ssid> <wifi_password>"
    exit 1
fi

module_file=$1
wifi_ssid=$2
wifi_password=$3

# 更新 wpa_supplicant.conf 文件
cat > /etc/wpa_supplicant.conf << EOF
network={
    ssid="$wifi_ssid"
    psk="$wifi_password"
}
EOF

# 加载驱动
insmod $module_file

# 启用网卡
ifconfig wlan0 up

# 连接到无线网络
wpa_supplicant -D nl80211 -i wlan0 -c /etc/wpa_supplicant.conf &

# 获取动态IP
udhcpc -i wlan0

# 测试是否联网
ping www.baidu.com
```

用法
```
./wifi.sh 8188eus.ko wifi-ssid wifi-password
```