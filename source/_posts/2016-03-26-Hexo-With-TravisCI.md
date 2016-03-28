---
title: Travs自动化部署Hexo
categories:
- 前端
- Hexo
tags:
- 前端
- Hexo
- 自动化
- Travis CI
date: 2016-03-26 20:55:29
---

>**本文介绍Hexo利用Travis CI自动化生成并发布,亲测可用.**

# 开通Travis CI
利用 GitHub账号登录 ** [Travis CI](https://travis-ci.org/) **

# 项目开启Travis CI

![use travis-ci][1]

在项目的设置中开启`Build only if .travis.yml is present`这一项.

![travis-ci setting][2]

# 在github中生成Access Token
>这个用于操作repo,否则没有权限.

![Profile Setting][3]

![Access Tokens][4]

# 安装Travis
>注意:需要安装Ruby,并且需要安装rubygems插件

``` shell
gem isntall travis
```

# 创建配置文件

在项目根目录创建`.travis.yml`文件
``` shell
touch .travis.yml
```

# 编辑配置文件
``` shell
language: node_js
branches:
  only:
  - master #源码分支名称
before_install:
- npm install -g hexo
- npm install -g hexo-cli
before_script:
- git config --global user.name 'yourname'
- git config --global user.email 'youremail'
- sed -i'' "s~git@github.com:<yourname>/<projectname>.git~https://${REPO_TOKEN}:x-oauth-basic@github.com/<yourname>/<projectname>.git~" _config.yml
install:
- npm install
script:
- hexo clean
- hexo generate
after_success:
- hexo deploy
```

# 配置Travis

* 登录travis
``` shell
travis login --auto
```

* 添加变量信息
在项目根目录下执行:
``` shell
travis encrypt 'REPO_TOKEN=<TOKEN>' --add
```
之后会在`.travis.yml`文件中添加下面的信息
``` shell
env:
  global:
    secure: fxBE17yzFhC2+FjwVLYbgIhggyfliv3dFCDozTJD7U3n...
```
>这里的`REPO_TOKEN`是变量名,在后面的配置文件中会用到.
>`TOKEN`是上面github生成的Token.

# 修改Hexo配置信息_config.yml
>如果之前配置过deploy信息可以略过.

``` shell
deploy:
  type: git
  repo: git@github.com:<yourname>/<projectname>.git
  branch: <branch>
```

# 测试效果
Push本地的代码至远程仓库，然后,在https://travis-ci.org看项目自动化执行.

原文地址:http://koyasu221b.com/2016/01/23/deploy-hexo-github-pages-by-travis/

[1]:/static/images/hexo-with-travisci.jpg
[2]:/static/images/hexo-with-travisci-setting.jpg
[3]:/static/images/20160328230629.jpg
[4]:/static/images/20160328230729.jpg
