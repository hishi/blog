---
title: "LinuxでCPU使用率を上げる"
date: 2019-07-21T16:32:33+09:00
draft: true
categories:
tags:
- linux
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---

<!--more-->

# CPU使用率を上げるコマンド

```bash
yes >> /dev/null
```

# yesコマンドとは？

`yes`コマンドは、killされるまで、y（または、引数で指定した文字列）を出力し続けるというもの。

```bash
YES(1)                     User Commands                         YES(1)

NAME
       yes - output a string repeatedly until killed

SYNOPSIS
       yes [STRING]...
       yes OPTION

DESCRIPTION
       Repeatedly output a line with all specified STRING(s), or 'y'.

       --help display this help and exit

       --version
              output version information and exit
```

# CPU使用率

2コアを割り当てた環境で`yes >> /dev/null`を実行すると`top`コマンドの結果は以下となった。

```bash
top - 08:32:26 up  2:26,  2 users,  load average: 0.64, 0.78, 1.01
Tasks: 160 total,   2 running,  95 sleeping,   0 stopped,   0 zombie
%Cpu(s): 47.9 us,  1.0 sy,  0.0 ni, 50.2 id,  0.3 wa,  0.0 hi,  0.5 si,  0.0 st
KiB Mem :  5831016 total,   638132 free,   322016 used,  4870868 buff/cache
KiB Swap:  4194300 total,  4194300 free,        0 used.  3419264 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
31269 root      20   0  107968    740    664 R  98.7  0.0   0:42.13 yes
30687 oracle    -2   0 2189636  58060  55164 S   2.0  1.0   0:04.22 ora_vktm_orcl
 3719 root      20   0  375512   3840   3344 S   0.3  0.1   0:02.99 VBoxService
```

コア毎の使用率に切り替えると、片方のコアが100%近い使用率となっている。

```bash
top - 08:34:43 up  2:28,  2 users,  load average: 1.11, 0.92, 1.02
Tasks: 159 total,   3 running,  93 sleeping,   0 stopped,   0 zombie
%Cpu0  : 98.4 us,  1.2 sy,  0.0 ni,  0.0 id,  0.0 wa,  0.0 hi,  0.4 si,  0.0 st
%Cpu1  :  0.3 us,  0.7 sy,  0.0 ni, 98.3 id,  0.0 wa,  0.0 hi,  0.7 si,  0.0 st
KiB Mem :  5831016 total,   646468 free,   313664 used,  4870884 buff/cache
KiB Swap:  4194300 total,  4194300 free,        0 used.  3427620 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
31269 root      20   0  107968    740    664 R  97.0  0.0   2:56.96 yes
30687 oracle    -2   0 2189636  58060  55164 S   3.3  1.0   0:07.33 ora_vktm_orcl
29188 root      20   0  154668   8960   7644 S   0.3  0.2   0:00.75 sshd
```


