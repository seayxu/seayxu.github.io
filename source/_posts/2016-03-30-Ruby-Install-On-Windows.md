---
title: 在Windows中搭建Ruby开发环境
date: 2016-03-30 22:49:09
categories:
- Ruby
tags:
- Ruby
---
# Windows中搭建Ruby开发环境教程
# 1. 下载RubyInstaller
   去[RubyInstaller.org](http://rubyinstaller.org/downloads/)官网中下载

# 2. 安装Ruby
   双击Ruby安装包 `RubyInstaller`,直接下一步操作就可以了。
   等安装完成,运行命令:`ruby -v`,显示版本号就说明安装成功。

# 3. 安装Devkit
   * 在[rubyinstaller.org](http://rubyinstaller.org/downloads/)上下载相对应版本的Devkit;
   * 解压下载的DevKit,选择解压的路径，这个路径就是DevKit的安装路径;
   * 进入到Devkit的目录,在命令窗口运行命令:`ruby dk.rb init`,将会产生一个配置文件`config.yml`;
   * 打开`config.yml`文件,将`ruby`的安装路径加上,格式是:`-+空格+ruby安装目录`,如下:`- C:\Program\Ruby\2.2.4`
   ![ruby-devkit-config.yml][1]
   * 然后执行安装命令`ruby dk.rb install`.

# 4. 安装RubyGems
   * 下载`RubyGems` package:
   [rubygems.org](https://rubygems.org/pages/download) [github.com](https://github.com/rubygems/rubygems/releases)

   * 解压下载的压缩包;
   * 进入解压的目录,执行安装命令`ruby setup.rb`,等待安装完成;
   * 安装完成后,执行命令`gem -v`,如果打印出版本号，即安装成功.

# 5. 收工
   至此,Ruby的开发环境基本完成,可以愉快的写`Hello World`了.

  [1]: https://segmentfault.com/img/bVtObG
