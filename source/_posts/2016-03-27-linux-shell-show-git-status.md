---
title: 在linux shell中显示git状态
date: 2016-03-27 23:07:25
categories:
- System
- Linux
tags:
- System
- Linux
- Ubuntu
- Shell
- Git
---

# Clone git source code

``` shell
git clone https://github.com/git/git.git ~/git
```

# Copy Bash and Shell script

>是指在git源码中`contrib/completion/`目录下的`git-completion.bash`和`git-prompt.sh`
>将这两个文件拷贝到指定目录,只要自己知道就好.
>在这里直接拷贝至用户目录~.

``` shell
#进入git源码目录
cd ~/git
#进入git源码completion目录
cd contrib/completion
# 拷贝git-completion.bash文件
cp git-completion.bash ~/.git-completion.sh
# 拷贝git-prompt.sh文件
cp git-prompt.sh ~/.git-prompt.sh
```

# Edit .bashrc file

``` shell
source ~/.git-completion.sh
source ~/.git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
export GIT_PS1_SHOWSTASHSTATE=1
export GIT_PS1_SHOWUNTRACKEDFILES=1
export GIT_PS1_SHOWUPSTREAM="verbose git svn"
PS1='\[\033[1;31m\]\u@\h \[\033[1;34m\]\W\[\033[1;31m\]$(__git_ps1 " (%s)")\[\033[1;35m\] -> \[\033[0m\]'
```

** 重启终端即可. **
