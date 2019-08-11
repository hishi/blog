---
title: "Oracleでディクショナリを調べる"
date: 2019-08-12T02:05:04+09:00
categories:
draft: false
tags:
- Oracle
keywords:
- tech
#thumbnailImage: //example.com/image.jpg
---

<!--more-->

ディクショナリ名がなんとなくしかわからない時に調べる方法。

```sql
SQL> select table_name from dictionary where table_name like 'DBA%PART%';

TABLE_NAME
--------------------------------------------------------------------------------
DBA_CUBE_SUB_PARTITION_LEVELS
DBA_HIVE_PART_KEY_COLUMNS
DBA_HIVE_TAB_PARTITIONS
DBA_IND_PARTITIONS
DBA_IND_SUBPARTITIONS
DBA_LOB_PARTITIONS
DBA_LOB_SUBPARTITIONS
DBA_MINING_MODEL_PARTITIONS
DBA_MVIEW_DETAIL_PARTITION
DBA_MVIEW_DETAIL_SUBPARTITION
DBA_PARTIAL_DROP_TABS
```

