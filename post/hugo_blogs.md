---
title: "使用 hugo 搭建静态网站"
date: 2020-04-08T11:22:12+08:00
draft: false 
tags: [
  'hugo',
  '静态网站'
]
categories: [
  "兴趣"
]
---
Hugo是由Go语言实现的静态网站生成器。  
简单、易用、高效、易扩展、快速部署。  

<!--more-->

## 创建网站  
```
hugo new site 路径  # 如: hugo new site /document/myblog
```
### 目录结构  
- config.toml : 网站的配置文件.  
- content : 文章存放的地方.  
- themes : 网站主题存放的地方.  
- stattic : 静态资源存放的地方, 如 图片, 样式文件, 脚本文件等, 对于文章中的图片, 建议使用专门的图床.  


## 选择主题  
- 通过命令行的方式使用主题: hugo -t 主题目录名  
- 通过在config.toml配置使用: theme = “主题目录名”  

## 创建/编写文章  
```
hugo new [路径]文章名.md
```
  `hugo new` 会创建包含默认元数据的文章.  
  在创建文章时, 如果没有路径, 文章会保存在 content 目录中, 如果包含路径则会在content目录中创建对应的目录.  
  `draft=true` 表示文章为草稿，在生成网站的时候不会生成页面.  

## 发布网站  
```
hugo -d 目标路径
```
- 如果不指定目标路径, 会默认在 **public** 目录下生成可部署的网站.  
- `hugo server -D` 本地生成网站预览.  
  默认地址为: `http://localhost:1313/` 如果 1313 端口被占用, 会随机生成其他的端口. -D(大写)参数作用是为草稿文件生成预览.  

