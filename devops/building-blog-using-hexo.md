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

## Setup theme - even
官方網站上面羅列了許多主題可供使用，這邊我們使用even 這個主題，並且安裝相關npm模組。
- download theme from GitHub

  ```
  $ cd themes/
  $ git clone https://github.com/ahonn/hexo-theme-even
  $ cd ..
  $ npm install --save hexo-renderer-jade hexo-generator-feed hexo-generator-sitemap hexo-browsersync hexo-generator-archive
  ```

- Edit configuration file `_config.yml`

  ```
  theme: even
  ```

## Advanced Usages
  - Archives
    edit `_config.yml`
    ```
    # Generate Archive
    archive_generator:
      per_page: 10
      yearly: true
      monthly: true
      daily: false
    ```
  - Pagination

    ```
    # Pagination
    ## Set per_page to 0 to disable pagination
    per_page: 10
    pagination_dir: page
    ```
  - Tags
    - add `tags` page
      `$ hexo new page tags`
    - edit `source/tags/index.md`, set layout to `tags`
      ```
      title: tags
      layout: tags
      ```
    - edit theme's `_config.yml`
      ```
      # ===========================================
      # Menu Settings
      # ===========================================
      menu:
        Home: /
        Archives: /archives/
        Tags: /tags
        Categories: /categories
        About: /about
      ```
  - Categories
    - add `categories` page
      `$ hexo new page categories`
    - edit `source/categories/index.md`, set layout to `categories`
      ```
      title: categories
      layout: categories
      ```
    - edit theme's `_config.yml`
      ```
      # ===========================================
      # Menu Settings
      # ===========================================
      menu:
        Home: /
        Archives: /archives/
        Tags: /tags
        Categories: /categories
        About: /about
      ```
  - about
    - add `about` page
      `$ hexo new page about`
    - edit `source/about/index.md`, adding some infomations
      ```
      title: categories
      ---
      # About Me
      My name is Helen
      ```
    - edit theme's `_config.yml`
      ```
      # ===========================================
      # Menu Settings
      # ===========================================
      menu:
        Home: /
        Archives: /archives/
        Tags: /tags
        Categories: /categories
        About: /about
      ```
  - image  
    If you want to add images in your posts, please place your images under `images` directory. And use markdown sytax `![](/img/test.jpg)`

    ![](/img/test.jpg)
  - read more link  
    在想要加入的地方加入`<!-- more -->`即可。
