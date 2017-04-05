---
title: 'Ubuntu: change username'
tags:
  - linux
  - ubuntu
categories:
  - IT
date: 2016-10-16 16:16:00
---

# Ubuntu change username
本篇文章以ubuntu 系統為例，說明如何更改現有的linux使用者名稱、群組及家目錄．

假設我們想要將現有的使用者`current_user` 改為 `new_user`，調整的步驟如下：

1. 顯示目前使用者的user、group、權限等資訊  

		id current_user  
		grep current_user /etc/passwd  
		grep current_user /etc/group  
		ls -ld /home/current_user  

2. 確認使用者current_user 的執行程序，如果有正在執行中的使用程序，中止相關程序。  

		ps aux | grep current_user
		ps -u current_user
		kill (-u current_user) pid
			
3. 更改目前使用者名稱，並且確認使用者  

		sudo usermod -l new_user current_user  
		id current_user  
		id new_user  
		
4. 更改目前使用者群組  

		sudo groupmod -n new_group current_group  
		id new_user    
	  
5. 更改家目錄  

		sudo usermod -d /home/new_user -m new_user  
		ls -ld /home/new/user  
			
這樣即完成了！要注意的是，如果有相關服務跑在家目錄底下的話，需要更改相關的config 檔中的絕對路徑設定！
