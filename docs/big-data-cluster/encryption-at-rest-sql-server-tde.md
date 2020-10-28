---
title: SQL Server 巨量資料叢集透明待用資料加密 (TDE) 使用指南
titleSuffix: SQL Server Big Data Clusters
description: 本文說明如何使用 BDC 的 SQL Server TDE 待用加密功能
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 55456185a6503ee11465a1e65cb9cd91de3ba6e2
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199559"
---
# <a name="sql-server-big-data-clusters-transparent-data-encryption-tde-at-rest-usage-guide"></a>SQL Server 巨量資料叢集透明待用資料加密 (TDE) 使用指南

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本指南示範如何使用 SQL Server 巨量資料叢集的待用加密功能來加密資料庫。

一般來說，此體驗會與 Linux 上的 SQL Server 相同，且適用[標準 TDE 文件](../relational-databases/security/encryption/transparent-data-encryption.md) (除非另有註明)。 若要監視主機上的加密狀態，請遵循 [`sys.dm_database_encryption_keys`](../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 和 [`sys.certificates`](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) 上的標準 DMV 查詢模式。

__不支援的功能：__
* 資料集區加密
* [HA 部署](deployment-high-availability.md)中所含可用性群組內資料庫的加密金鑰輪替。


## <a name="prerequisites"></a><a id="prereqs"></a> 必要條件

- [SQL Server 巨量資料叢集 CU8+](release-notes-big-data-cluster.md)
- [巨量資料工具](deploy-big-data-tools.md)
   - **Azure Data Studio**
- 具有系統管理權限的 SQL Server 使用者。

## <a name="query-the-installed-certificates"></a>查詢已安裝的憑證

1. 在 Azure Data Studio 中，連線到巨量資料叢集的 SQL Server 主要執行個體。 如需詳細資訊，請參閱[連線到 SQL Server 主要執行個體](connect-to-big-data-cluster.md#master)。

1. 按兩下 [伺服器]  視窗中的連線，顯示 SQL Server 主要執行個體的伺服器儀表板。 選取 [新增查詢]  。

   ![SQL Server 主要執行個體查詢](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 執行下列 Transact-SQL 命令，將內容變更為主要執行個體中的 **master** 資料庫。

   ```sql
   USE master
   GO
   ```

1. 查詢已安裝的系統管理憑證。 

   ```sql
    SELECT TOP 1 name FROM sys.certificates WHERE name LIKE 'TDECertificate%' ORDER BY name DESC
   ```

    視需要使用不同的查詢準則。

    憑證名稱會以 "TDECertificate{timestamp}" 的形式列出。 當您看到前置詞為 TDECertificate，而後面接著時間戳記時，這就是系統管理功能所提供的憑證。

## <a name="encrypt-a-database-using-the-system-provided-certificate"></a>使用系統提供的憑證來加密資料庫

在下列範例中，根據上一節的輸出，假設有名為 __userdb__ 的資料庫作為加密目標，以及名為 __TDECertificate2020_09_15_22_46_27__ 的系統提供憑證。

1. 請使用下列模式，透過所提供的系統憑證來產生資料庫加密金鑰。

   ```sql
    USE userdb; 
    GO
    CREATE DATABASE ENCRYPTION KEY WITH ALGORITHM = AES_256 ENCRYPTION BY SERVER CERTIFICATE TDECertificate2020_09_15_22_46_27;
    GO
   ```

1. 使用下列命令來加密資料庫 __userdb__ 。

   ```sql
    ALTER DATABASE userdb SET ENCRYPTION ON;
    GO
   ```

## <a name="next-steps"></a>後續步驟

了解 HDFS 的待用加密：
> [!div class="nextstepaction"]
> [HDFS 加密區域](encryption-at-rest-hdfs-encryption-zones.md)
