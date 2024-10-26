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


# 联网脚本
touch wifi.sh

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
./wifi.sh module-file wifi-ssid wifi-password
```