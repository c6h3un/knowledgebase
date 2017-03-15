---
title: Fortigate Login security issue
tags:
  - network
  - firewall
categories:
  - IT
date: 2017-03-15 15:54
---
使用fortigate的時候，有觀察到會有惡意ip過來嘗試登入fortigate的狀況，因此會希望在防火牆上面加上一些安全措施。

下面紀錄兩種方式來增加安全度：

- 設定管理帳號登入 ACL
UI登入> System > Admin > Administrator > account > 設定trusted host。


- 使用Cli設定帳號登入的嘗試次數及鎖定時間

```
  config system global
    set admin-lockout-threshold 3
    set admin-lockout-duration 600
  end
```

#### Reference
- [Technical Tip : How to prevent brute force attempts to a FortiGate administrator account login](http://kb.fortinet.com/kb/documentLink.do?externalID=FD32198)
- [Configuring Administrator access to a FortiGate unit using Trusted Hosts](http://kb.fortinet.com/kb/documentLink.do?popup=true&externalID=10868&languageId=)
