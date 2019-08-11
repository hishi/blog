---
title: "VirtualBoxでよく使うコマンド"
date: 2019-08-12T01:21:27+09:00
categories:
draft: false
tags:
- VirtualBox
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---

<!--more-->


# VM一覧表示
```bash
VBoxManage list vms
```

# VM一覧表示（起動中のVMのみ）

```bash
VBoxManage list runningvms
```

# VM操作

## VM停止

```bash
VBoxManage controlvm ora12201 acpipowerbutton
```

## VM起動

```bash
VBoxManage startvm ora12201 --type headless
```

## NWアダプタ追加

```bash
VBoxManage modifyvm ora12201 --nic3 hostonly
VBoxManage modifyvm ora12201 --hostonlyadapter3 "VirtualBox Host-Only Ethernet Adapter #5"
```

## NWアダプタ削除

```bash
VBoxManage modifyvm ora12201 --nic3 none
```

## ポートフォワーディング

```bash
# 設定追加
VBoxManage controlvm ora12201 natpf1 "test,tcp,127.0.0.1,2222,,22"

# 確認
VBoxManage showvminfo ora12201 | grep NIC | grep Rule

# 設定削除
VBoxManage controlvm ora12201 natpf1 delete "test"
```

# スナップショット

## スナップショット作成

```bash
VBoxManage snapshot ora12201 take "test"
```

## スナップショット削除

```bash
VBoxManage snapshot ora12201 delete "test"
```

## スナップショット表示

```bash
VBoxManage snapshot ora12201 list
```

## スナップショットリストア

```bash
VBoxManage snapshot ora12201 restore "test"
```


