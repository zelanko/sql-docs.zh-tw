---
title: 還原資料庫
titleSuffix: SQL Server big data clusters
description: 本文示範如何將資料庫還原至 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]的主要執行個體。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 925254bbdc7200b5e7ca2a3c413de87e8915b2b4
ms.sourcegitcommit: 335d27d0493ddf4ffb770e13f8fe8802208d25ae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2020
ms.locfileid: "81002717"
---
# <a name="restore-a-database-into-the-sql-server-big-data-cluster-master-instance"></a>將資料庫還原至 SQL Server 巨量資料叢集的主要執行個體

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文示範如何將現有資料庫還原至 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]的主要執行個體。 建議的方法是使用備份、複製和還原方法。

## <a name="backup-your-existing-database"></a>備份現有的資料庫

首先，從 Windows 或 Linux 上的 SQL Server 備份現有的 SQL Server 資料庫。 搭配 Transact-SQL 或 SQL Server Management Studio (SSMS) 等工具使用標準備份技術。

本文說明如何還原 AdventureWorks 資料庫，但您可以使用任意資料庫備份。 

> [!TIP]
> 下載 [AdventureWorks 備份](../samples/adventureworks-install-configure.md)。

## <a name="copy-the-backup-file"></a>複製備份檔案

將備份檔案複製到 Kubernetes 叢集之主要執行個體 Pod 中的 SQL Server 容器。

```bash
kubectl cp <path to .bak file> master-0:/tmp -c mssql-server -n <name of your big data cluster>
```

範例：

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n clustertest
```

接著，確認備份檔案已複製到 Pod 容器。

```bash
kubectl exec -it master-0 -n <name of your big data cluster> -c mssql-server -- bin/bash
cd /var/
ls /tmp
exit
```

範例：

```bash
kubectl exec -it master-0 -n clustertest -c mssql-server -- bin/bash
ls /tmp
exit
```

## <a name="restore-the-backup-file"></a>還原備份檔案

接下來，將資料庫備份還原至 SQL Server 主要執行個體。  如果您想要還原在 Windows 上建立的資料庫備份，您必須取得檔案的名稱。  在 Azure Data Studio 中，連線到主要執行個體並執行此 SQL 指令碼：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/<db file name>.bak'
```

範例：

```sql
RESTORE FILELISTONLY FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
```

![備份檔案清單](media/restore-database/database-restore-file-list.png)

現在，還原資料庫。 以下為範例指令碼。 請根據您的資料庫備份，視需要取代名稱/路徑。

```sql
RESTORE DATABASE AdventureWorks2016CTP3
FROM DISK='/tmp/AdventureWorks2016CTP3.bak'
WITH MOVE 'AdventureWorks2016CTP3_Data' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Data.mdf',
        MOVE 'AdventureWorks2016CTP3_Log' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_Log.ldf',
        MOVE 'AdventureWorks2016CTP3_mod' TO '/var/opt/mssql/data/AdventureWorks2016CTP3_mod'
```

## <a name="configure-data-pool-and-hdfs-access"></a>設定資料集區和 HDFS 存取

現在，若要讓 SQL Server 主要執行個體存取資料集區和 HDFS，請執行資料集區和存放集區預存程序。 對您剛還原的資料庫執行下列 Transact-SQL 指令碼：

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
> 您只需要針對從舊版 SQL Server 還原的資料庫執行這些安裝指令碼。 如果您在 SQL Server 主要執行個體中建立新的資料庫，會為您設定好資料集區和存放集區預存程序。

## <a name="next-steps"></a>後續步驟

若要深入了解 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]，請參閱下列概觀：

- [什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
