---
title: 開始使用 Linux 上的 SQL Server 的效能功能 |Microsoft Docs
description: 這篇文章介紹 SQL Server 效能功能的 SQL server 的 Linux 使用者。 許多這些範例作用於所有平台，但這篇文章的內容是 Linux。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.custom: sql-linux
ms.openlocfilehash: 91a83740d83cb6e121d8ea413cf6322f75b68dff
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001850"
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>在 Linux 上的 SQL Server 的效能功能的逐步解說

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

如果您是剛接觸 SQL Server 的 Linux 使用者時，下列工作會引導您完成一些效能功能。 這些不是唯一或特定 Linux，但它有助於讓您了解區域以進一步調查。 在每個範例中，會提供該區域的深度文件的連結。

> [!NOTE]
> 下列範例使用 AdventureWorks 範例資料庫。 如需有關如何取得並安裝這個範例資料庫的指示，請參閱 <<c0> [ 從 Windows 的 SQL Server 資料庫還原到 Linux](sql-server-linux-migrate-restore-database.md)。

## <a name="create-a-columnstore-index"></a>建立資料行存放區索引
資料行存放區索引是一種技術來儲存及查詢大型存放區中稱為資料行存放區的單欄式資料格式的資料。  

1. 加入 SalesOrderDetail 資料表的資料行存放區索引來執行下列 TRANSACT-SQL 命令：

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. 執行下列查詢使用掃描資料表的資料行存放區索引：

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. 確認資料行存放區索引，使用查閱的 object_id 資料行存放區索引，並確認它會出現在 SalesOrderDetail 資料表的使用方式統計資料：

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>使用記憶體內部 OLTP
SQL Server 提供記憶體內部 OLTP 功能，可大幅提升應用程式系統的效能。  評估指南的這個章節將逐步引導您逐步完成建立記憶體最佳化的資料表，儲存在記憶體和原生編譯的預存程序，才能存取資料表，而不必編譯或解譯。

### <a name="configure-database-for-in-memory-oltp"></a>設定資料庫以使用記憶體內部 OLTP
1. 建議您將資料庫設定為至少 130 使用記憶體內部 OLTP 的相容性層級。  您可以使用下列查詢來檢查 AdventureWorks 的目前相容性層級：  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   如有必要，請更新層級為 130:

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. 當交易涉及磁碟基礎的資料表和記憶體最佳化的資料表時，它的基本操作交易隔離等級的交易的記憶體最佳化部分的名稱為快照集。  若要可靠地強制執行記憶體最佳化的資料表，在跨容器交易中的這個層級，請執行下列作業︰

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. 您可以建立之前記憶體最佳化的資料表，您必須先建立記憶體最佳化檔案群組和資料檔案的容器：

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>建立記憶體最佳化資料表
記憶體最佳化資料表的主要存放區是主記憶體，因此，不同於以磁碟為基礎的資料表，資料不需要在從磁碟讀取到記憶體緩衝區。  若要建立記憶體最佳化的資料表，請使用 MEMORY_OPTIMIZED = ON 子句。

1. 執行下列查詢來建立記憶體最佳化的資料表 dbo。ShoppingCart。  做為預設值，資料會保存為持久性用途 （請注意，持久性也可以設定要保存僅限結構描述） 的磁碟上。 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. 某些記錄插入資料表中：

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>原生編譯的預存程序
SQL Server 支援原生編譯的預存程序存取記憶體最佳化資料表。 T-SQL 陳述式會編譯成機器碼，並儲存成原生 Dll，啟用更快速的資料存取與更有效率的查詢執行，比傳統的 T-SQL。   標示為 NATIVE_COMPILATION 的預存程序為原生編譯。 

1. 執行下列指令碼來建立原生編譯的預存程序 ShoppingCart 資料表中插入大量的記錄：


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
查詢存放區會收集查詢、 執行計畫和執行階段統計資料的詳細的效能資訊。

查詢存放區不是作用中，依預設，而且可以使用 ALTER DATABASE 加以啟用：

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

執行下列查詢來傳回查詢存放區中的查詢與計劃的相關資訊： 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>查詢動態管理檢視
動態管理檢視會傳回可用來監視伺服器執行個體的健康情況、 診斷問題和調整效能的伺服器狀態資訊。

若要查詢 dm_os_wait 統計資料的動態管理檢視：

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
