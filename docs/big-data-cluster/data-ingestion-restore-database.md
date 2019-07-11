---
title: 還原資料庫
titleSuffix: SQL Server big data clusters
description: 這篇文章會示範如何將資料庫還原到 SQL Server 2019 巨量資料叢集 （預覽） 的主要執行個體。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ba16d0c0fa04460199ece151509b8567bdd947f9
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728991"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>將資料庫還原到 SQL Server 巨量資料叢集主要執行個體

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何將現有的資料庫還原至 SQL Server 2019 巨量資料叢集 （預覽） 的主要執行個體。 建議的方法是使用備份、 複製和還原方法。

## <a name="backup-your-existing-database"></a>您現有的資料庫備份

首先，備份您現有的 SQL Server 資料庫從 SQL Server 在 Windows 或 Linux。 使用 TRANSACT-SQL 或工具等 SQL Server Management Studio (SSMS)，請使用標準的備份技術。

本文說明如何還原 AdventureWorks 資料庫中，但您可以使用任何的資料庫備份。 

> [!TIP]
> 您可以下載 AdventureWorks 備份[此處](https://www.microsoft.com/download/details.aspx?id=49502)。

## <a name="copy-the-backup-file"></a>將備份檔案複製

將備份檔案複製到 SQL Server 容器的 Kubernetes 叢集的主要執行個體 pod 中。

```bash
kubectl cp <path to .bak file> mssql-master-pool-0:/tmp -c mssql-server -n <name of your big data cluster>
```

範例

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n clustertest
```

然後，確認備份檔案已複製到 pod 容器。

```bash
kubectl exec -it mssql-master-pool-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

範例

```bash
kubectl exec -it mssql-master-pool-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>備份檔案還原

接下來，在主要執行個體 SQL Server 還原資料庫備份。  如果您要還原的資料庫備份，建立在 Windows 上，您必須取得檔案的名稱。  在 Azure 資料 Studio 中，連接到主要執行個體，並執行下列 SQL 指令碼：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

範例

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![備份的檔案清單](media/restore-database/database-restore-file-list.png)

現在，將資料庫還原。 下列指令碼是範例。 取代所需視您資料庫的備份名稱/路徑。

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>設定資料集區和 HDFS 的存取

現在，若要存取資料集區和 HDFS 的 SQL Server 主要執行個體，執行資料集區和儲存體集區預存程序。 針對您剛還原的資料庫執行下列 TRANSACT-SQL 指令碼：

```sql
USE AdventureWorks2016CTP3
GO
-- Create the SqlDataPool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
  CREATE EXTERNAL DATA SOURCE SqlDataPool
  WITH (LOCATION = 'sqldatapool://controller-svc/default');

-- Create the SqlStoragePool data source:
IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
   CREATE EXTERNAL DATA SOURCE SqlStoragePool
   WITH (LOCATION = 'sqlhdfs://controller-svc/default');
GO
```

> [!NOTE]
> 您必須執行的資料庫從舊版的 SQL Server 還原這些設定指令碼。 如果您在 SQL Server 的主要執行個體中建立新的資料庫，您已設定資料集區和儲存體集區預存程序。

## <a name="next-steps"></a>後續步驟

若要深入了解 SQL Server 巨量資料叢集，請參閱下列概觀：

- [什麼是 SQL Server 2019 巨量資料叢集？](big-data-cluster-overview.md)
