---
title: 開始使用 Linux 上的 SQL Server 效能功能
description: 本文為剛開始使用 SQL Server 的 Linux 使用者提供 SQL Server 效能功能簡介。 其中許多範例適用於所有平台，但本文內容的適用對象為 Linux。
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.openlocfilehash: fe60b00654d93c6362a8671318a4b7b88ae90a5f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "67896167"
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>Linux 上的 SQL Server 效能功能逐步解說

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

如果您是剛開始使用 SQL Server 的 Linux 使用者，下列工作將逐步解說一些效能功能。 這不是 Linux 專屬或特別的功能，但可協助您大致了解哪些領域需要深入了解。 在每個範例中，會提供該領域的深入文件連結。

> [!NOTE]
> 下列範例使用 AdventureWorks 範例資料庫。 如需如何取得和安裝此範例資料庫的指示，請參閱[將 SQL Server 資料庫從 Windows 還原到 Linux](sql-server-linux-migrate-restore-database.md)。

## <a name="create-a-columnstore-index"></a>建立資料行存放區索引
資料行存放區索引是以單欄式資料格式，儲存和查詢大型資料存放區 (稱為資料行存放區) 的一項技術。  

1. 執行下列 Transact-SQL 命令，將資料行存放區索引新增至 SalesOrderDetail 資料表：

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. 執行下列查詢，使用資料行存放區索引掃描資料表：

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. 藉由查閱資料行存放區索引的 object_id，並確認它出現在 SalesOrderDetail 資料表的使用統計資料中，來確認資料行存放區索引已在使用中：

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>使用記憶體內部 OLTP
SQL Server 提供記憶體內部 OLTP 功能，可大幅改進應用程式系統的效能。  評估指南的這個章節將逐步引導您建立儲存在記憶體中經記憶體最佳化的資料表，以及可存取資料表而不需要進行編譯或解譯的原生編譯預存程序。

### <a name="configure-database-for-in-memory-oltp"></a>設定記憶體內部 OLTP 的資料庫
1. 建議將資料庫的相容性層級設定為 130 以上，以便使用記憶體內部 OLTP。  使用下列查詢，檢查目前 AdventureWorks 的相容性層級：  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   如果需要，請將層級更新為 130：

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. 當交易同時涉及以磁碟為基礎的資料表和經記憶體最佳化的資料表時，很重要的一點是交易的記憶體最佳化部分需在名為 SNAPSHOT 的交易隔離等級中執行。  在跨容器交易中，若要能穩定地對經記憶體最佳化的資料表強制執行此等級，請執行下列程式碼：

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. 在您能夠建立經記憶體最佳化的資料表之前，您必須先為資料檔案建立經記憶體最佳化的檔案群組和容器：

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>建立經記憶體最佳化的資料表
經記憶體最佳化的資料表之主要存放區是主記憶體，因此不同於以磁碟為基礎的資料表，資料不需要從磁碟讀入記憶體緩衝區。  若要建立經記憶體最佳化的資料表，請使用 MEMORY_OPTIMIZED = ON 子句。

1. 執行下列查詢，建立經記憶體最佳化的資料表 dbo.ShoppingCart。  根據預設，基於持久性目的，資料會保存在磁碟上 (請注意，DURABILITY (持久性) 也可以設定為只保存結構描述)。 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. 在資料表中插入一些記錄：

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>原生編譯的預存程序
SQL Server 支援原生編譯預存程序，可存取經記憶體最佳化的資料表。 T-SQL 陳述式會編譯成機器碼並儲存為原生 DLL，提供比傳統 T-SQL 更快速的資料存取與更有效率的查詢執行。   標示為 NATIVE_COMPILATION 的預存程序為原生編譯。 

1. 執行下列指令碼，建立原生編譯的預存程序，以在 ShoppingCart 資料表中插入大量記錄：


   ```sql
   CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int 
    WITH NATIVE_COMPILATION, SCHEMABINDING AS 
   BEGIN ATOMIC 
   WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

   DECLARE @i int = 0

   WHILE @i < @InsertCount 
    BEGIN 
     INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL) 
     SET @i += 1 
    END
   END 
   ```
2. 插入 1,000,000 個資料列：

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. 確認已插入資料列：

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>深入了解記憶體內部 OLTP
如需記憶體內部 OLTP 的詳細資訊，請參閱下列主題：

- [快速入門 1：可讓 Transact-SQL 擁有更快效能的記憶體內部 OLTP 技術](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [移轉至 In-Memory OLTP](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [使用記憶體最佳化加快暫存資料表與資料表變數的速度](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [監視與疑難排解記憶體使用量](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [In-Memory OLTP (記憶體中最佳化)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>使用查詢存放區
查詢存放區會收集有關查詢、執行計畫和執行階段統計資料的詳細效能資訊。

查詢存放區預設不會啟用，並可使用 ALTER DATABASE 加以啟用：

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

執行下列查詢，傳回查詢存放區中查詢和計畫的相關資訊： 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>查詢動態管理檢視
動態管理檢視會傳回伺服器狀態資訊，這項資訊可用來監視伺服器執行個體的健全狀況、診斷問題和調整效能。

若要查詢 dm_os_wait stats 動態管理檢視：

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
