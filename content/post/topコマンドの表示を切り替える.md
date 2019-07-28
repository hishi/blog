---
title: "topコマンドの表示を切り替える"
date: 2019-07-21T15:14:26+09:00
categories:
draft: false
tags:
- linux
- top
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---

<!--more-->

# topコマンドとは？

topコマンドは、Linuxのリソース使用率を確認するコマンドである。
OS全体やプロセス毎のCPU/メモリ使用率を表示することができる。

# topコマンドの実行結果

topコマンドを普通に（オプションなど指定せずに）実行した場合は以下のような表示となる。
1行目～5行目がOS全体の値、6行目以降がプロセス毎の値を示している。

```bash
top - 06:55:16 up 49 min,  2 users,  load average: 0.93, 0.35, 0.13
Tasks: 110 total,   2 running,  46 sleeping,   0 stopped,   0 zombie
%Cpu(s):  1.3 us, 12.9 sy,  0.0 ni, 77.7 id,  7.6 wa,  0.0 hi,  0.5 si,  0.0 st
KiB Mem :  5831016 total,  2720940 free,   608932 used,  2501144 buff/cache
KiB Swap:  4194300 total,  4194300 free,        0 used.  4910124 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
10472 oracle    20   0 4768128 555600  25704 S  75.4  9.5   1:08.17 java
10473 root      20   0       0      0      0 I   2.3  0.0   0:00.07 kworker/u4:1
10404 root      20   0       0      0      0 I   1.0  0.0   0:00.21 kworker/1:1
   16 root      20   0       0      0      0 S   0.3  0.0   0:00.33 ksoftirqd/1
 3719 root      20   0  375512   3840   3344 S   0.3  0.1   0:01.02 VBoxService
12122 root      20   0  162024   4392   3684 R   0.3  0.1   0:00.05 top
    1 root      20   0  128104   8368   5800 S   0.0  0.1   0:03.77 systemd
    2 root      20   0       0      0      0 S   0.0  0.0   0:00.01 kthreadd
    4 root       0 -20       0      0      0 I   0.0  0.0   0:00.00 kworker/0:0H
    6 root       0 -20       0      0      0 I   0.0  0.0   0:00.00 mm_percpu_wq
 ...省略...
```

# topコマンドの表示切り替える

## h

ヘルプを表示する。

```bash
Help for Interactive Commands - procps-ng version 3.3.10
Window 1:Def: Cumulative mode Off.  System: Delay 3.0 secs; Secure mode Off.

  Z,B,E,e   Global: 'Z' colors; 'B' bold; 'E'/'e' summary/task memory scale
  l,t,m     Toggle Summary: 'l' load avg; 't' task/cpu stats; 'm' memory info
  0,1,2,3,I Toggle: '0' zeros; '1/2/3' cpus or numa node views; 'I' Irix mode
  f,F,X     Fields: 'f'/'F' add/remove/order/sort; 'X' increase fixed-width

  L,&,<,> . Locate: 'L'/'&' find/again; Move sort column: '<'/'>' left/right
  R,H,V,J . Toggle: 'R' Sort; 'H' Threads; 'V' Forest view; 'J' Num justify
  c,i,S,j . Toggle: 'c' Cmd name/line; 'i' Idle; 'S' Time; 'j' Str justify
  x,y     . Toggle highlights: 'x' sort field; 'y' running tasks
  z,b     . Toggle: 'z' color/mono; 'b' bold/reverse (only if 'x' or 'y')
  u,U,o,O . Filter by: 'u'/'U' effective/any user; 'o'/'O' other criteria
  n,#,^O  . Set: 'n'/'#' max tasks displayed; Show: Ctrl+'O' other filter(s)
  C,...   . Toggle scroll coordinates msg for: up,down,left,right,home,end

  k,r       Manipulate tasks: 'k' kill; 'r' renice
  d or s    Set update interval
  W,Y       Write configuration file 'W'; Inspect other output 'Y'
  q         Quit
          ( commands shown with '.' require a visible task display window )
Press 'h' or '?' for help with Windows,
Type 'q' or <Esc> to continue
```

## 1

コア毎の使用率に切り替える。再度`1`を押すと元の表示に戻る。

```bash
top - 07:10:38 up  1:04,  2 users,  load average: 0.00, 0.17, 0.27
Tasks: 110 total,   2 running,  47 sleeping,   0 stopped,   0 zombie
%Cpu0  :  0.3 us,  1.0 sy,  0.0 ni, 98.3 id,  0.0 wa,  0.0 hi,  0.3 si,  0.0 st
%Cpu1  :  0.3 us,  0.0 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  5831016 total,   186308 free,   743016 used,  4901692 buff/cache
KiB Swap:  4194300 total,  4194300 free,        0 used.  4721948 avail Mem
```

## u

表示対象ユーザを絞る。

`Which user (blank for all)`のようにユーザ名の指定が求められるので対象ユーザ名を入力する。

```bash
top - 07:44:52 up  1:38,  2 users,  load average: 1.08, 0.48, 0.27
Tasks: 148 total,   2 running,  84 sleeping,   0 stopped,   0 zombie
%Cpu(s): 50.4 us,  4.4 sy,  0.0 ni, 39.5 id,  5.0 wa,  0.0 hi,  0.7 si,  0.0 st
KiB Mem :  5831016 total,   118360 free,   568068 used,  5144588 buff/cache
KiB Swap:  4194300 total,  4194300 free,        0 used.  3163964 avail Mem
Which user (blank for all)
```

## M

メモリ使用率順にソートする。

```bash
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
32402 oracle    20   0 2189380 306180 303520 S   0.0  5.3   0:00.32 ora_mman_orcl
32453 oracle    20   0 2218196 189468 162064 S   0.0  3.2   0:02.70 ora_mmon_orcl
32491 oracle    20   0 2200808 102628  92324 S   0.7  1.8   0:01.48 ora_cjq0_orcl
32711 oracle    20   0 2196404  98728  90952 S   0.3  1.7   0:00.52 ora_q002_orcl
```

## P

CPU使用率順にソートする（デフォルト）。

```bash
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
32396 oracle    -2   0 2189376  57896  55224 S   2.9  1.0   0:04.44 ora_vktm_orcl
  435 root      20   0  162024   4428   3676 R   1.0  0.1   0:00.12 top
32491 oracle    20   0 2200808 102628  92324 S   0.7  1.8   0:01.53 ora_cjq0_orcl
    8 root      20   0       0      0      0 I   0.3  0.0   0:03.56 rcu_sched
```

## T

実行時間順にソートする。

```bash
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
    1 root      20   0  128104   7752   5184 S   0.0  0.1   0:07.28 systemd
 1493 root      20   0       0      0      0 S   0.0  0.0   0:04.68 xfsaild/dm-0
32396 oracle    -2   0 2189376  57896  55224 S   0.7  1.0   0:04.52 ora_vktm_orcl
    8 root      20   0       0      0      0 I   0.0  0.0   0:03.56 rcu_sched
```


## c

プロセスのパスや引数を含めた表示に切り替える。

```bash
  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
27388 oracle    20   0 2341864 894884 829576 R  96.4 15.3  21:56.45 oracleorcl (DESCRIPTION=(LOCAL=YES)(ADDRESS=(PR+
26650 oracle    20   0 3254532 369032  36512 S   0.3  6.3   1:04.54 /u01/app/oracle/product/12.2.0/dbhome_1/jdk/jre+
27257 oracle    -2   0 2189636  57820  54928 S   3.0  1.0   0:35.45 ora_vktm_orcl
27231 oracle    20   0  119664  26712  19572 S   0.3  0.5   0:31.99 /u01/app/oracle/product/12.2.0/dbhome_1/bin/sql+
```

## k

プロセスを kill する。

`PID to signal/kill [default pid = 24867]`のようにPIDの指定を求められるので入力する。
デフォルトでは、先頭のプロセスのPIDが指定された状態となる。
なお、プロセスの kill をやめる場合は、`ESC`を押す。

```bash
top - 07:19:04 up  1:12,  3 users,  load average: 0.45, 0.22, 0.21
Tasks: 112 total,   2 running,  49 sleeping,   0 stopped,   0 zombie
%Cpu(s): 47.0 us,  0.5 sy,  0.0 ni, 51.9 id,  0.0 wa,  0.0 hi,  0.5 si,  0.0 st
KiB Mem :  5831016 total,   166700 free,   746804 used,  4917512 buff/cache
KiB Swap:  4194300 total,  4194300 free,        0 used.  4717420 avail Mem
PID to signal/kill [default pid = 24867]
```

PIDを指定した後は、`Send pid 24867 signal [15/sigterm]`のようにシグナルの指定が求められる。
デフォルトでは、15(プロセスの終了)が指定された状態となる。

```bash
top - 07:19:04 up  1:12,  3 users,  load average: 0.45, 0.22, 0.21
Tasks: 112 total,   2 running,  49 sleeping,   0 stopped,   0 zombie
%Cpu(s): 47.0 us,  0.5 sy,  0.0 ni, 51.9 id,  0.0 wa,  0.0 hi,  0.5 si,  0.0 st
KiB Mem :  5831016 total,   166700 free,   746804 used,  4917512 buff/cache
KiB Swap:  4194300 total,  4194300 free,        0 used.  4717420 avail Mem
Send pid 24867 signal [15/sigterm]
```

