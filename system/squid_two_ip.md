---
title: Squid Proxy two outgoing ip config
tags:
  - network
  - proxy
categories:
  - IT
date: 2017-02-22 22:47
---

### 使用情境
Squid server 上面有配置了兩個內網ip 兩個公網ip 分別提供不同用途：

| Nic  | IP          | usage                      |
|------|-------------|----------------------------|
| eth0 | 10.0.12.10  | 10.0.12.0/24 網段proxy服務  |
| eth1 | 10.0.10.10  | 10.0.10.0/24 網段proxy服務  |
| eth2 | 1.1.1.1     | 一般外部訪問                 |
| eth3 | 2.2.2.2     | 連github, google api       |

### 監聽不同的內網ip


### 設定外部訪問策略
