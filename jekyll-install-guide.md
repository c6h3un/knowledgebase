---
title: Jekyll Installation Guide
tags:
  - Jekyll
  - static site generator
categories:
  - web
---
## Jekyll Installation Guide

### Install Steps  
- install pre  
	`sudo apt-get install -y ruby2.0 ruby2.0-dev nodejs`
- install jekyll using gem  
	`sudo gem install jekyll`


### 除錯
1. 出現下面error:`sh: 1: make: not found`
`sudo apt-get install make`
2. 出現下面錯誤訊息  
 	
  ```
  /usr/bin/ruby1.9.1 extconf.rb
  /usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in 'require': cannot load such file -- mkmf (LoadError)
  from /usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in 'require'
  from extconf.rb:4:in '<main>'
  ```  

  `sudo apt-get install ruby-dev `

3. 出現下面錯誤訊息：

  ```	
  ERROR:  Error installing jekyll:
  jekyll requires Ruby version >= 2.0.0.
  ```  

  ```  
  [helen@server~$ sudo gem2.0 install jekyll  

  Building native extensions.  This could take a while...
  Successfully installed ffi-1.9.14
  Fetching: rb-inotify-0.9.7.gem (100%)
  Successfully installed rb-inotify-0.9.7
  .
  ..
  ...
  7 gems installed
  ```  	

