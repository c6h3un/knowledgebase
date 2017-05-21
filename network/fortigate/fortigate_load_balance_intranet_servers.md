---
title: Fortigate Load balance intranet servers
tags:
  - network
  - firewall
categories:
  - IT
date: 2017-05-21 21:23
---
Cause we don't have a f5 for load balancing server in alpha environment. So I decide to use fortigate for intranet server load balancing. Here's are the example

### Use Case  
Two servers needed for load balancing, with 1 virtual server ip in the same intranet.  

| Name       | IP          | Netmask       | interface |
|------------|-------------|---------------|-----------|
| worker-1   | 10.0.112.25 | 255.255.255.0 | dmz       |
| worker-2   | 10.0.112.26 | 255.255.255.0 | dmz       |
| worker-vip | 10.0.112.10 | 255.255.255.0 | dmz       |

allow access from network `10.0.80.0/22` and network `10.0.112.0/24`.  

### Firewall informations  
| Name            | informations        |
|-----------------|---------------------|
| Model           | FG140D              |
| Operation Mode  | Standalone          |
| HA Status       | NAT                 |
| Firmware Version| v5.0,build4235 (GA) |

### Configuration Steps  

- Create Health Check `icmp-ping`  
 - Open `Firewall Objects > Load Balance > Health Check`, and click `Create New`, fill in the infomations:  

| Name               | Informations |
|--------------------|--------------|
| Name               | icmp-ping    |
| Type               | PING         |
| Interval           | 10           |
| Timeout            | 2            |
| Retry              | 3            |

- Create Virtual Server `worker-vip`  
  - Open `Firewall Objects > Load Balance > Virtual Server`, and click `Create New`, fill in the infomations:  
  
| Name               | Informations        |
|--------------------|---------------------|
| Name               | worker-vip          |
| Type               | IP                  |
| Interface          | dmz                 |
| Virtual Server IP  | 10.0.112.10         |
| Load Balance Method| Round Robbin        |
| Health Check       | icmp-ping           |

- Create Real Server `worker-1`, `worker-2`  
 - Open `Firewall Objects > Load Balance > Real Server`, under worker-vip click `Create New`, fill in the infomations.  
  - add worker-1  

| Name               | Informations        |
|--------------------|---------------------|
| IP Adderss         | 10.0.112.25         |
| Max Connections    | 100                 |
| Mode               | Active              |

  - add worker-2   

| Name               | Informations        |
|--------------------|---------------------|
| IP Adderss         | 10.0.112.26         |
| Max Connections    | 100                 |
| Mode               | Active              |
- Create Policy 

| Name               | Informations        |
|--------------------|---------------------|
| Policy Type        | Firewall            |
| Policy Subtype     | Address             |
| Incoming Interface | dmz                 |
| Source Address     | all                 |
| Outgoing Interface | dmz                 |
| Destination Address| worker-vip          |
| Schedule           | always              |
| Service            | all                 |
| Action             | accept              |

`Enable NAT > Use Destination Interface`  

#### Reference  
- [Load balancing configuration examples](http://help.fortinet.com/fos50hlp/54/Content/FortiOS/fortigate-load-balancing-52/ldb_examples.htm)
