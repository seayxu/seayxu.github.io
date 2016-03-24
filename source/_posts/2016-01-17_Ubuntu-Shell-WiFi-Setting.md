---
title: Ubuntu(Shell)命令行下连接到无线网络-使用wpa-cli命令
date: 2016-01-17 19:16:20
categories:
- System
- Linux
- Ubuntu

tags:
- Ubuntu
- Raspberry Pi 2
- 树莓派
---

# 情景说明

> 自己买了个`Raspberry Pi 2`的板子，没有显示器，想利用无线连接通过`SSH`连接。无奈之下才上网查了下，发现可以利用`shell`命令设置无线连接，于是，就有了以下的内容。

# 动手实施

## 步骤

1. 在`shell`中输入`wpa_cli`命令，进入交互，然后输入以下信息(注：#为注释)

2. 设置相关信息

  ```
  add_network #执行后会返回一个数字（一般是0）
  #network_id为无线网的ID，自己取名
  set_network [network_id] ssid '无线名称' #根据你的网络环境填写
  set_network [network_id] psk '无线密码' #无线密码
  enable_network [network_id] #启用网络，成功后会返回 CONNECT TO XXXX的信息
  ```

3. 退出交互模式

  输入`q`退出交互模式。

4. 连接网络

  使用 `dhclient wlan0` 命令获取网络地址。

# 示例

  ```
  root@ubuntu:~$ ifconfig #查看无线网卡名称，假定为nxthswrw234
  root@ubuntu:~$ wpa_cli
  add_network
  set_network NETID ssid 'MyWiFi'
  set_network NETID psk '12345678'
  enable_network NETID
  q
  root@ubuntu:~$ dhclient nxthswrw234 #nxthswrw234为无线网卡名称
  ```
