---
title: mssqlctl 儲存體掛接參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 儲存體命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3ad8a97bac1f708dcf01612368c76d584fa39f5c
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860289"
---
# <a name="mssqlctl-storage-mount"></a>mssqlctl storage mount

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**儲存體掛接**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [建立](#create) | 在 HDFS 中的遠端存放區的掛接。 |
| [刪除](#delete) | 刪除掛接在 HDFS 中的遠端存放區。 |
| [status](#status) | Mount(s) 的狀態。 |

## <a id="create"></a> mssqlctl storage mount create

在 HDFS 中的遠端存放區的掛接。

```
mssqlctl storage mount create
   --local-path
   --remote-uri
   [--credential-file]
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--local-path** | HDFS 路徑掛上必須為建立 （掛上的目的地）。 必要。 |
| **--remote-uri** | 要掛接 （來源掛接） 的遠端存放區的 URI。 必要。 |
| **--credential-file** | 包含的認證來存取遠端存放區的檔案。 認證必須指定為索引鍵 = 值 」 配對一個索引鍵 = 每行的值。 任何在索引鍵或值的 equals 必須逸出。 預設為必要項無認證。 必要的金鑰，取決於所掛接的遠端存放區的類型和授權使用的類型。 |

### <a name="examples"></a>範例

HDFS 路徑上掛接第 2 代 ADLS 帳戶 」 adlsv2example 」 中的容器 「 資料 」`/mounts/adlsv2/data`使用共用的金鑰：

```
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/ --local-path /mounts/adlsv2/data --credentials credential_file
```

若要裝載遠端 HDFS 叢集 (`hdfs://namenode1:8080/`) 上本機 HDFS 路徑`/mounts/hdfs/`:

```
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --local-path /mounts/hdfs/
```

## <a id="delete"></a> mssqlctl storage mount delete

刪除掛接在 HDFS 中的遠端存放區。

```
mssqlctl storage mount delete
   --local-path
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--local-path** | 對應至掛接的 HDFS 路徑的已遭刪除。 必要。 |

### <a name="examples"></a>範例

刪除掛接端建立 /mounts/adlsv2/data 第 2 代 ADLS 儲存體帳戶。

```
mssqlctl storage mount delete --local-path /mounts/adlsv2/data
```

## <a id="status"></a> mssqlctl storage mount status

Mount(s) 的狀態。

```
mssqlctl storage mount status
   --local-path
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