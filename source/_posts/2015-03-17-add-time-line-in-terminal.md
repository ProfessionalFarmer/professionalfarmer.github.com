---
title: 为OSX和Linux的TERMINAL增加时间分割线
tags:
  - Linux
  - Mac
url: archives/753.html
id: 753
categories:
  - Default Category
date: 2015-03-17 05:56:44
---
Add a Handy Separator Between Commands in Your Terminal on Mac OS X and Linux
为终端的命令行之间添加时间线，增加可读性，效果如下。

```
Last login: Tue Mar 17 13:18:30 on ttys000
----------------------------------------------------------------------- 13:32:37
zzx@zzxdesk:~$ pwd
/Users/zzx
----------------------------------------------------------------------- 13:38:31
zzx@zzxdesk:~$ cd Desktop/
----------------------------------------------------------------------- 13:38:40
zzx@zzxdesk:~/Desktop$ pwd
/Users/zzx/Desktop
----------------------------------------------------------------------- 13:38:42
zzx@zzxdesk:~/Desktop$
```

<!--more-->

首先备份home下的.bash_profile： cp .bash_profile .bash_profile_bak
编辑.bash_profile，添加如下内容
```
 ############################################
 # Modified from emilis bash prompt script
 # from https://github.com/emilis/emilis-config/blob/master/.bash_ps1
 #
 # Modified for Mac OS X by
 # @corndogcomputer
 ###########################################
 # Fill with minuses
# (this is recalculated every time the prompt is shown in function prompt_command):

fill="--- "

reset_style='[33[00m]'

status_style=$reset_style'[33[0;90m]' # gray color; use 0;37m for lighter color

prompt_style=$reset_style

command_style=$reset_style'[33[1;29m]' # bold black

# Prompt variable:

PS1="$status_style"'$fill tn'"$prompt_style"'${debian_chroot:+($debian_chroot)}u@h:w$'"$command_style "

# Reset color for command output

# (this one is invoked every time before a command is executed):

trap 'echo -ne "33[00m"' DEBUG

function prompt_command {

# create a $fill of all screen width minus the time string and a space:

let fillsize=${COLUMNS}-9

fill=""

while [ "$fillsize" -gt "0" ]

do

fill="-${fill}" # fill with underscores to work on

let fillsize=${fillsize}-1

done

# If this is an xterm set the title to user@host:dir

case "$TERM" in

xterm*'rxvt*)

bname=`basename "${PWD/$HOME/~}"`

echo -ne "33]0;${bname}: ${USER}@${HOSTNAME}: ${PWD/$HOME/~}07"

;;

*)

;;

esac

}

PROMPT_COMMAND=prompt_command
```

保存，重新启动Terminal终端即可看到效果。

对于Linux用户，需要将上面的代码贴到home文件夹中的.bashrc文件中，如果没有请先创建这个文件。