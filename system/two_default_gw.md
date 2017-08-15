---
title: Setting up two default gateway for linux server
tags:
  - network
  - routing
categories:
  - IT
date: 2017-02-21 22:47
---

這幾天在接入兩個ISP 到  server，希望讓外部client 從哪個wan ip連進來就由哪個interface回。
因此這邊需要讓server有兩張routing table 分別設定default gw。

## Informations  

| Interface | IP      | Netmask       | Gateway IP   | Default ISP  |
|-----------|---------|---------------|--------------|--------------|
| p1p1      | 1.1.1.1 | 255.255.255.0 | 1.1.1.254    | v            |
| p1p2      | 1.1.2.2 | 255.255.255.0 | 1.1.2.254    |              |

## Steps  
1. Add routing table
```
sudo vim /etc/iproute2/rt_tables
---
1 wan2
```

2. Edit network configurations
```
sudo vim /etc/network/interfaces
---
auto p1p1
iface p1p1 inet static
	address 1.1.1.1
	netmask 255.255.255.0
	gateway 1.1.1.254
	dns-nameservers 8.8.8.8

auto p1p2
iface p1p2 inet static
	address 1.1.2.2
	netmask 255.255.255.0
	post-up ip route add 1.1.2.0/24 dev p1p2 src 1.1.2.2 table wan2
	post-up ip route add default via 1.1.2.254 dev p1p2 table wan2
	post-up ip rule add from 1.1.2.2/32 table wan2
	post-up ip rule add to 1.1.2.2/32 table wan2
---
```

3. Start p1p2
`sudo ifup p1p2`

4. Check
```
ip route list table wan2
ip rule show
```

## Reference
- https://www.thomas-krenn.com/en/wiki/Two_Default_Gateways_on_One_System
