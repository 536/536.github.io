---
title: Add virtual-ip in wsl
date: 2024-07-05 20:35:53
tags:
    - wsl
    - network
---

有这么一个需求，在wsl中需要默认添加一个虚拟网卡，指向192.168.10.6/24。即：

```bash
ifconfig eth0:1 192.168.10.6/24
```

找了一圈最好的办法还是设置一个服务专门添加这个网卡，在此记录一下。

```
# /etc/systemd/system/virtual-ip.service
[Unit]
Description=Set up virtual IP address
After=network.target

[Service]
Type=oneshot
ExecStart=ifconfig eth0:1 192.168.10.6/24

[Install]
WantedBy=multi-user.target
```
