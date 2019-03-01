---
title: mssqlctl 儲存體掛接參考
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 儲存體命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8580c3c52cda484581f1c88ccfc039d8bd0bf78
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018454"
---
# <a name="mssqlctl-storage-mount"></a>mssqlctl 儲存體掛接

下列文章提供的參考**儲存體掛接**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [create](#create) | 在 HDFS 中的遠端存放區的掛接。 |
| [delete](#delete) | 刪除掛接在 HDFS 中的遠端存放區。 |
| [status](#status) | Mount(s) 的狀態。 |

## <a id="create"></a> mssqlctl storage mount create

在 HDFS 中的遠端存放區的掛接。

```
mssqlctl storage mount create
   --mount-path
   --remote-uri
   [--credential-file]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--mount-path** | HDFS 路徑掛上必須為建立 （掛上的目的地）。 必要。 |
| **--remote-uri** | 要掛接 （來源掛接） 的遠端存放區的 URI。 必要。 |
| **--credential-file** | 包含的認證來存取遠端存放區的檔案。 認證必須指定為索引鍵 = 值 」 配對一個索引鍵 = 每行的值。 任何在索引鍵或值的 equals 必須逸出。 預設為必要項無認證。 必要的金鑰，取決於所掛接的遠端存放區的類型和授權使用的類型。 |

### <a name="examples"></a>範例

HDFS 路徑上掛接第 2 代 ADLS 帳戶 」 adlsv2example 」 中的容器 「 資料 」`/mounts/adlsv2/data`使用共用的金鑰：

```
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/ --mount-path /mounts/adlsv2/data --credentials credential_file
```

若要裝載遠端 HDFS 叢集 (`hdfs://namenode1:8080/`) 上本機 HDFS 路徑`/mounts/hdfs/`:

```
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```

## <a id="delete"></a> mssqlctl storage mount delete

刪除掛接在 HDFS 中的遠端存放區。

```
mssqlctl storage mount delete
   --mount-path
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--mount-path** | 對應至掛接的 HDFS 路徑的已遭刪除。 必要。 |

### <a name="examples"></a>範例

刪除掛接端建立 /mounts/adlsv2/data 第 2 代 ADLS 儲存體帳戶。

```
mssqlctl storage mount delete --mount-path /mounts/adlsv2/data
```

## <a id="status"></a> mssqlctl storage mount status

Mount(s) 的狀態。

```
mssqlctl storage mount status
   --mount-path
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--mount-path** | 掛接路徑。 必要。 |

### <a name="examples"></a>範例

取得以路徑掛接狀態

```
mssqlctl storage mount status --mount-path /mounts/hdfs
```

取得所有掛接的狀態。

```
mssqlctl storage mount status
```

## <a name="next-steps"></a>後續步驟

如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。