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
0. 在windows上msvc的后端汇编质量最好，mingw只能是个玩具，个人学习，个人项目以及跨平台可以用mingw，其他后端用msvc
1. 最近在折腾c++的opencv，发现windows上cmake，vcpkg默认都是msvc工具链，如果要用mingw，需要我们修改配置为mingw工具链
2. 官网以及scoop下载的windows的opencv，都是msvc版本，但是opencv的mingw版本与msvc版本有区别，mingw版本的需要我们手动编译才能使用
3. 有时候动态库找不到入口，找不到动态库，编译器不对，可能是忘记添加到path以及path优先级不对（cmake生成的mingw配置文件中clang覆盖了gcc）（gcc环境重值到环境变量首位,莫名解决了dll找不到入口问题,也有可能是将动态库添加到了系统级path，提高了了动态库优先级）
4. 如果要使用windows上的cl，第一个实在在vs中使用，第二在terminal的选项卡中用，第三是在cmd中用
 "C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\Common7\Tools\VsDevCmd.bat" -startdir=none -arch=x64 -host_arch=x64 激活（pwsh也有相应选项），第四将msvc的bin，lib，include添加到path，第5使用clang-cl替代cl兼容大部分cl编译情况。
 5. 巨坑，vcpkg安装的其他项目可以正常识别，vcpkg安装成功了msvc的opencv，但无论如何都提示找不到，不管是set vcpkg目录还是直接opencv目录,vcpkg安装mingw-oencv失败。opencv msvc（cl，clang）无论如何都安装不上，opencv，mingw可以安装成功。windows msvc好像是与vcpkg冲突了，windows是c++二等公民，c++优先linux或wsl2，编程大多数推荐linux，wsl2.
 6. 安装c，c++软件从源码编译，默认用release模式，如果安装的是编译工具，选release模式没问题，用它构建的程序可以调试，因为这个release意思是你构建这个开发的工具的过程是release，你不能调试这个过程，而不是用这个程序链接后的产品release，这个产品可以自己选择release，debug，而克隆的源代码因为我们只是使用它，不是它的开发人员（开发这个项目本身以及给他开发配套服务或者对他进行性能分析，我们只是用它开发自己的程序），用release模式，只有我们给开发这个项目本身以及给他开发配套服务或者对他进行性能分析，才用debug