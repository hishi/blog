---
title: "コマンドラインでVirtualBoxゲストにISOファイルを接続する"
date: 2019-07-28T23:40:04+09:00
drafts: false
categories:
tags:
- VirtualBox
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---

<!--more-->

# やりたいこと

タイトル通り。 
コマンドライン（VBoxManage）でVirtual BoxゲストにISOファイルを接続する。
GUIを起動するのが面倒な場合のメモ。

# コマンド

## ストレージ・インタフェース名確認

```bash
# ストレージ・インタフェース名確認
$ VBoxManage showvminfo ora12201 | grep "Storage Controller Name"
Storage Controller Name (0):            IDE Controller 
Storage Controller Name (1):            SATA Controller

# ポート番号、デバイス番号確認
$ VBoxManage showvminfo ora12201 | grep IDE
Storage Controller Name (0):            IDE Controller
IDE Controller (0, 0): Empty
```

## ISOファイル接続

```bash
# ISOファイル接続
$ VBoxManage storageattach ora12201 --storagectl 'IDE Controller' --port 0 --device 0 --type dvddrive --medium /w/_home/media/OracleLinux/7.2/V100082-01.iso

# ISOファイル接続確認
$ VBoxManage showvminfo ora12201 | grep "IDE"
Storage Controller Name (0):            IDE Controller
IDE Controller (0, 0): W:\_home\media\OracleLinux\7.2\V100082-01.iso (UUID: ca9296f0-870a-4ae0-92a3-0bcfad0906c7)
```


## ISOファイル切断

```bash
# ISOファイル切断
$ VBoxManage storageattach ora12201 --storagectl 'IDE Controller' --port 0 --device 0 --type dvddrive --medium emptydrive --forceunmount

# ISOファイル切断確認
$ VBoxManage showvminfo ora12201 | grep IDE
Storage Controller Name (0):            IDE Controller
IDE Controller (0, 0): Empty
```



