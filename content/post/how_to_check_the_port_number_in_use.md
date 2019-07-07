---
title: "ポート番号を使用しているプロセスを確認する"
date: 2019-07-07
draft: false
categories:
tags:
- Linux
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---

<!--more-->

`netstat`コマンドでプロセスID（PID）を確認した後に`ps`コマンドでプロセス名を特定する。

# プロセスIDを確認する

まず、`netstat`コマンドで、ポート番号22を使用しているプロセスIDを確認する。

```bash
[root@localhost ~]# netstat -anp | grep :22
tcp        0      0 0.0.0.0:22                  0.0.0.0:*                   LISTEN      1837/sshd
tcp        0      0 10.0.2.15:22                10.0.2.2:54297              ESTABLISHED 1930/sshd
tcp        0      0 :::22                       :::*                        LISTEN      1837/sshd
```

上記結果から、ポート番号22を使用しているプロセスIDは`1837`と`1930`であることがわかる。

# プロセス名を特定する

次に、`ps`コマンドで、プロセスIDが`1837`と`1930`のプロセス名を特定する。

```bash
[root@localhost ~]# ps -ef | grep -e 1930 -e 1837
root      1837     1  0 23:30 ?        00:00:00 /usr/sbin/sshd
root      1930  1837  0 23:34 ?        00:00:00 sshd: root@pts/1
root      1937  1930  0 23:34 pts/1    00:00:00 -bash
root      2012  1937  0 23:57 pts/1    00:00:00 grep -e 1930 -e 1837
```

上記結果から、ポート番号22を使用しているプロセスは`/usr/sbin/sshd`と`sshd: root@pts/1`であることがわかる。

