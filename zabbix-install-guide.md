---
title: Zabbix Server and Zabbix Agent Install Guide  
tags:
 - monitor
 - zabbix
categories:
 - Ops
date: 2016-12-14 11:45
---
### Preparation  

> * zabbix server binary  
> * zabbix server configuration  
> * General Infomations: hostname, IP...   
> * Monitoring target infomation & templates  
> * Zabbix user & group infomations  
> * alert scripts  
> * zabbix agent binary  
> * zabbix agent config  

### General Infomation  
> * machine role: zabbix server  
> * Hostname: zabbix-server  
> * Machine IP: 10.128.112.10  

## General Steps of zabbix server  
1. get zabbix packages  
2. install zabbix-server with database, frontend, and java gateway  
3. Create initial database on MySQL or Postgres  
4. Edit zabbix server configuration  
	`sudo vim /etc/zabbix/zabbix_server.conf`
5. Start Zabbix server process.  
	`sudo service zabbix-server start`  
6. Editing PHP configuration for Zabbix frontend   
	`sudo vim /etc/apache2/conf-enabled/zabbix.conf`
	
	```
	php_value date.timezone Asia/Taipei
	```
7. Restart apache web server  
	`sudo service apache2 restart`  
8. Accessing `http://10.128.112.10/zabbix` using your browser  


### Create initial database - Postgres  

1. change to user postgres  
	`sudo su postgres`  
2. login to  
	
	```
	shell> psql -U postgres -d template1
	template1=# create database zabbix;
	template1=# CREATE USER zabbix WITH PASSWORD 'zbx_PASS';
	template1=# GRANT ALL PRIVILEGES ON DATABASE zabbix TO zabbix;
	template1=# \q
	```
3. Then import initial schema and data.  

	```
	(edit /etc/passwd /bin/false to /bin/bash)
	sudo su zabbix 
	psql -U zabbix zabbix < schema.sql 
	psql -U zabbix zabbix < images.sql 
	psql -U zabbix zabbix < data.sql 
	```
ps. The _schema.sql_, _images.sql_, _data.sql_ scripts can be found at _database/postgresql/_ directory under the source packages  

### Check Point
* Check zabbix server is up  
	`ps aux |grep 'zabbix_server: poller'`  
* Check server ipmi poller is up  
	`ps aux |grep 'zabbix_server: ipmi poller'`  
* Check server java poller is up  
	`ps aux |grep 'zabbix_server: java poller'`  
* Check server runs normally in web UI  
* Timeout setting in zabbix server conf = 30  

### Examples
* zabbix server configuration

	```
	DBHost=localhost
	DBName=zabbix
	DBUser=zabbix
	DBPassword=zbx_PASS
	Timeout=30
	LogFileSize=512
	JavaGateway=127.0.0.1
	StartPollers=20
	StartIPMIPollers=5
	StartJavaPollers=5
	StartSNMPTrapper=1
	
	```

### Trouble Shooting

* During configuring web, if php database support not showing PostgreSQL  
  `sudo apt-get install php5-pgsql`  

* If zabbix server not started, check your _zabbix server configuration_  
	* `ps aux |grep zabbix`  
	* `vim /etc/zabbix/zabbix_server.conf`  
	* `sudo su zabbix; zabbix_server` and see the error messages.  
* Check handly using `zabbix_get`


## General Steps of zabbix agent
* Ubuntu   
	1. Install zabbix agent 
	`sudo apt-get install zabbix-agent`  
	2. Edit /etc/zabbix/zabbix_agend.conf
	3. Restart zabbix agent

* Windows  
	1. Download [zabbix-agent for windows](http://www.zabbix.com/downloads/3.0.0/zabbix_agents_3.0.0.win.zip)	
	2. unzip file into directory `E:\zabbix_agents_3.0.0.win\`
	3. cd into `E:\zabbix_agents_3.0.0.win\conf\` and edit the config file `zabbix_agentd.win.conf`
	4. cd into `E:\zabbix_agents_3.0.0.win\win32\` and install zabbix agent with the config file using `zabbix_agentd.exe -c E:\zabbix_agents_3.0.0.win\conf\zabbix_agentd.win.conf --install
	5. start zabbix agent using `zabbix_agentd.exe --start`

### Check Point
* Check agent is up  
	`ps aux |grep zabbix_agentd`  
* Log into _zabbix web_ to see the latest data of your server


	
