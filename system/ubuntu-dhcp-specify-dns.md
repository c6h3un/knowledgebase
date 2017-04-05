---
title: Setting up dns server for ubuntu server using dhcp
tags:
  - network
categories:
  - IT
date: 2017-04-05 21:07
---

### 使用情境
在做系統設定時，DHCP取得ip時所提供的 dns server並不合用，需要設定使用額外的dns server 以及自定義的search domain來提供內部服務使用。下面為設定範例。

* server /etc/network/interfaces config  

  ```  
  auto eth0  
  iface eth0 inet dhcp  
  ```  

* server dhcp 取得的dns namserver  
  `/etc/resolv.conf`  

  ```  
  nameserver 8.8.8.8  
  nameserver 8.8.4.4  
  ```  

* 額外自行架設的dns server 資訊  
 * dns ip - **10.1.1.1**  
 * dns search domain - **helen.localnet**  

### 設定方式
- 編輯`/etc/dhcp/dhclient.conf`檔案，新增下面

  ```
  supersede domain-name "helen.localnet";
  prepend domain-name-servers 10.1.1.1;
  ```

- 重啟網卡  
  `sudo ifdown eth0 && sudo ifup eth0`  

- 確認設定檔  
  `cat /etc/resolv.conf`  

  ```
  nameserver 10.1.1.1
  nameserver 8.8.8.8
  nameserver 8.8.4.4
  search helen.localnet
  ```  

- 測試dns 
  `nslookup pc.helen.localnet`  
  `dig +short pc.helen.localnet`  

