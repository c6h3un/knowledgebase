---
title: Backup Active Directory servers in Windows Server 2012r2
tags:
  - windows server 2012r2
  - AD
categories:
  - IT
---
### Install Windows Server Backup
- Open _Add roles and features wizard_ in Server Dashboard

- Select _Windows Server Backup_ in Features step


### Config Server Backup

#### Backup to NAS

- Preparation
	- NAS IP
	- Backup Path
	- Connection Method
	- (Optional) authentication account & password
- Select _Tool>Windows Server Backup_ in Server Dashboard to open up the tool
- Select _Backup Once_ for testing or _Backup Schedule_ for regular backup
- Select Next
- Select Custom , Next
- Add Item > System State
- OK > Next
- Remote Shared Folder
- enter path
- username & password
- backup

