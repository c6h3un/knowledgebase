---
title: Building markdown into hexo site
tags:
 - hexo
categories:
 - blog
date: 2017-02-01 18:33
---

本篇文章記錄如何hexo將markdown文件產生成方便讀的靜態網頁。

## Installation

- install hexo-cli
要安裝hexo-cli 首先請先安裝nodejs 以及他的套件管理工具 npm。
再利用下面指令安裝hexo-cli 即可。
`npm install -g hexo-cli`
- install theme into `themes` folder
官方網站上面羅列了許多主題可供使用，這邊我們使用even 這個主題，並且安裝相關npm模組。

```
$ cd themes/
$ git clone https://github.com/ahonn/hexo-theme-even
$ cd ..
$ npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive
```
- Edit configuration file `_config.yml`

## Advanced functions
  - pagination
  - tags
  - categories
  - about
