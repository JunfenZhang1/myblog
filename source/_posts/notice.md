---
title: notice
date: 2024-12-28 06:08:57
pinned: 50
sticky: 50
tags:
categories: notice
---

## 文档，维基，github readme

学一个东西先看文档，小项目在readme

中型搜索文档，大型看维基（搜索 项目+docs，也有的直接放在github界面code区右上角的链接处）

## 反代的坑
1. nginx proxy_pass路径带/与不带/有重大区别，带/可以example1/blog->example2/(example1/blog/path->example2/path)，不带/只能example1/blog->example2/blog
2. 我部署的博客反代正常，但是跳转出现了问题，他是对/的绝对路径，不是对于当前位置的相对路径,这种情况不要用带/反代，在博客项目中可以调整root为/blog/（与反代url一致），或者直接新开一个域名（/开始反代）
3. clouflare rule（origin rule）也可以反代


## c++的坑
1.最近在折腾c++的opencv，发现windows上cmake，vcpkg默认都是msvc工具链，如果要用mingw，需要我们修改配置为mingw工具链
2.官网以及scoop下载的windows的opencv，都是msvc版本，但是opencv的mingw版本与msvc版本有区别，mingw版本的需要我们手动编译才能使用