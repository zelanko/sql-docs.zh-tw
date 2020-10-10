---
title: 應用程式模式 - 分割記憶體最佳化資料表
description: 了解記憶體內部 OLTP 應用程式設計模式，其會將目前作用中的資料儲存在記憶體最佳化資料表中，並將較舊的資料儲存在資料分割資料表中。
ms.custom: seo-dt-2019,issue-PR=4700-14820
ms.date: 05/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 3f867763-a8e6-413a-b015-20e9672cc4d1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 08fb58f77382dae2d6455cc181c983798c89050a
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529409"
---
# <a name="application-pattern-for-partitioning-memory-optimized-tables"></a>分割記憶體最佳化資料表的應用程式模式

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[hek_2](../../includes/hek-2-md.md)] 支援應用程式設計模式，可為較新的資料大量提供效能資源。 當目前資料的讀取或更新頻率高於較舊資料時，即可套用此模式。 在此情況下，我們會將目前的資料稱作「作用中」或「經常性」資料，而較舊的資料則稱為「非經常性」資料。

此模式的主要概念是將「經常性」資料儲存在記憶體最佳化資料表中。 轉變為「非經常性」的較舊資料會在每週或每月移至分割資料表。 分割資料表會將其資料儲存在磁碟或其他硬碟，而非記憶體中。

這種設計通常會使用 **datetime** 索引鍵，以讓移動程序能夠有效率地區分經常性與非經常性資料。

## <a name="advanced-partitioning"></a>進階分割

此設計會模擬為分割資料表，該分割資料表也會具有記憶體最佳化分割區。 若要讓這種設計能夠正常執行，則必須確定所有資料表全都共用通用的結構描述。 本文稍後的程式碼範例會說明這項技術。

新的資料會依定義假設為經常性資料。 經常性資料會在記憶體最佳化資料表中插入及更新。 非經常性資料則會保留在傳統分割資料表中。 預存程序會定期新增新的分割區。 該分割區會包含最近已移出記憶體最佳化資料表的非經常性資料。

如果作業只需要經常性資料，則可使用原生編譯的預存程序來存取資料。 可能會存取經常性或非經常性資料的作業必須使用已解譯 [!INCLUDE[tsql](../../includes/tsql-md.md)]，以將記憶體最佳化資料表與分割資料表聯結在一起。

### <a name="add-a-partition"></a>新增分割區

最近轉變為非經常性的資料必須移動到分割資料表中。 這種定期分割交換的步驟如下所示：

1. 若為記憶體最佳化資料表中的資料，則會判斷日期時間，該日期時間是經常性資料與新非經常性資料之間的界限或截止時間。
2. 將來自記憶體內部 OLTP 資料表的新非經常性資料插入 *cold\_staging* 資料表中。
3. 刪除記憶體最佳化資料表中的相同非經常性資料。
4. 將 cold\_staging 資料表交換至資料分割區。
5. 新增分割區。

#### <a name="maintenance-window"></a>維護時間範圍

其中一個先前步驟是從記憶體最佳化資料表中刪除新的非經常性資料。 此刪除動作與最後一個步驟 (新增分割區) 之間存在一段時間間隔。 在此間隔期間，所有應用程式皆無法讀取新的非經常性資料。

如需相關範例，請參閱 [應用程式層級資料分割](../../relational-databases/in-memory-oltp/application-level-partitioning.md)。

## <a name="code-sample"></a>程式碼範例

為方便展示，下列 Transact-SQL 範例會顯示在一段較小的程式碼區塊中。 您可將其全部附加到大型的程式碼區塊中，以供測試之用。

整體而言，T-SQL 範例會示範如何使用具有分割磁碟型資料表的記憶體最佳化資料表。

T-SQL 範例的第一階段會建立資料庫，然後在該資料庫中建立資料表之類的物件。 後續階段則會示範如何將資料從記憶體最佳化資料表移至分割資料表。

### <a name="create-a-database"></a>建立資料庫

在此區段中，T-SQL 範例會建立測試資料庫。 該資料庫會設定為同時支援記憶體最佳化資料表與資料分割資料表。

```sql
CREATE DATABASE PartitionSample;
GO

-- Add a FileGroup, enabled for In-Memory OLTP.
-- Change file path as needed.

ALTER DATABASE PartitionSample
    ADD FILEGROUP PartitionSample_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE PartitionSample
    ADD FILE(
        NAME = 'PartitionSample_mod',
        FILENAME = 'c:\data\PartitionSample_mod')
    TO FILEGROUP PartitionSample_mod;
GO
```

### <a name="create-a-memory-optimized-table-for-hot-data"></a>建立經常性資料的記憶體最佳化資料表

此區段會建立記憶體最佳化資料表，包含最新的資料，而其中大多為經常性資料。

```sql
USE PartitionSample;
GO

-- Create a memory-optimized table for the HOT Sales Order data.
-- Notice the index that uses datetime2.

CREATE TABLE dbo.SalesOrders_hot (
   so_id INT IDENTITY PRIMARY KEY NONCLUSTERED,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL INDEX ix_date NONCLUSTERED,
   so_total MONEY NOT NULL,
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) WITH (MEMORY_OPTIMIZED=ON);
GO
```

### <a name="create-a-partitioned-table-for-cold-data"></a>建立非經常性資料的資料分割資料表

此區段會建立保存非經常性資料的分割資料表。

```sql
-- Create a partition and table for the COLD Sales Order data.
-- Notice the index that uses datetime2.

CREATE PARTITION FUNCTION [ByDatePF](datetime2) AS RANGE RIGHT
   FOR VALUES();
GO

CREATE PARTITION SCHEME [ByDateRange]
   AS PARTITION [ByDatePF]
   ALL TO ([PRIMARY]);
GO

CREATE TABLE dbo.SalesOrders_cold (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date DATETIME2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc)
) ON [ByDateRange](so_date);
GO
```

### <a name="create-a-table-to-store-cold-data-during-move"></a>在移動期間建立資料表以儲存非經常性資料

此區段會建立 cold\_staging 資料表。 同時也會建立結合兩個資料表中經常性資料與非經常性資料的檢視。

```sql
-- A table used to briefly stage the newly cold data, during moves to a partition.

CREATE TABLE dbo.SalesOrders_cold_staging (
   so_id INT NOT NULL,
   cust_id INT NOT NULL,
   so_date datetime2 NOT NULL,
   so_total MONEY NOT NULL,
   CONSTRAINT PK_SalesOrders_cold_staging PRIMARY KEY (so_id, so_date),
   INDEX ix_date_total NONCLUSTERED (so_date desc, so_total desc),
   CONSTRAINT CHK_SalesOrders_cold_staging CHECK (so_date >= '1900-01-01')
);
GO

-- A view, for retrieving the aggregation of hot plus cold data.

CREATE VIEW dbo.SalesOrders
AS SELECT so_id,
          cust_id,
          so_date,
          so_total,
          1 AS 'is_hot'
       FROM dbo.SalesOrders_hot
   UNION ALL
   SELECT so_id,
          cust_id,
          so_date,
          so_total,
          0 AS 'is_cold'
       FROM dbo.SalesOrders_cold;
GO
```

### <a name="create-the-stored-procedure"></a>建立預存程序

此區段會建立定期執行的預存程序。 此程序會將新的非經常性資料從記憶體最佳化資料表移至分割資料表。

```sql
-- A stored procedure to move all newly cold sales orders data
-- to its staging location.

CREATE PROCEDURE dbo.usp_SalesOrdersOffloadToCold @splitdate datetime2
   AS
   BEGIN
      BEGIN TRANSACTION;

      -- Insert the cold data as a temporary heap.
      INSERT INTO dbo.SalesOrders_cold_staging WITH (TABLOCKX)
      SELECT so_id , cust_id , so_date , so_total
         FROM dbo.SalesOrders_hot WITH (serializable)
         WHERE so_date <= @splitdate;

      -- Delete the moved data from the hot table.
      DELETE FROM dbo.SalesOrders_hot WITH (SERIALIZABLE)
         WHERE so_date <= @splitdate;

      -- Update the partition function, and switch in the new partition.
      ALTER PARTITION SCHEME [ByDateRange] NEXT USED [PRIMARY];

      DECLARE @p INT = (
        SELECT MAX(partition_number)
            FROM sys.partitions
            WHERE object_id = OBJECT_ID('dbo.SalesOrders_cold'));

      EXEC sp_executesql
        N'ALTER TABLE dbo.SalesOrders_cold_staging
            SWITCH TO dbo.SalesOrders_cold partition @i',
        N'@i int',
        @i = @p;

      ALTER PARTITION FUNCTION [ByDatePF]()
      SPLIT RANGE( @splitdate);

      -- Modify a constraint on the cold_staging table, to align with new partition.
      ALTER TABLE dbo.SalesOrders_cold_staging
         DROP CONSTRAINT CHK_SalesOrders_cold_staging;

      DECLARE @s nvarchar( 100) = CONVERT( nvarchar( 100) , @splitdate , 121);
      DECLARE @sql nvarchar( 1000) = N'alter table dbo.SalesOrders_cold_staging 
         add constraint CHK_SalesOrders_cold_staging check (so_date > ''' + @s + ''')';
      PRINT @sql;
      EXEC sp_executesql @sql;

      COMMIT;
END;
GO
```

### <a name="prepare-sample-data-and-demo-the-stored-procedure"></a>準備範例資料，並示範預存程序

此區段會產生並插入範例資料，然後示範執行預存程序。

```sql
-- Insert sample values into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(1,SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(1, SYSDATETIME(), 1);
GO

-- Verify that the hot data is in the table, by selecting from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Treat all data in the hot table as cold data:
-- Run the stored procedure, to move (offload) all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Again, read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Retrieve the name of every partition.
SELECT OBJECT_NAME( object_id) , * FROM sys.dm_db_partition_stats ps
   WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold');

-- Insert more data into the hot table.
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO
INSERT INTO dbo.SalesOrders_hot VALUES(2, SYSDATETIME(), 1);
GO

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, run the stored procedure, to move all sales orders to date to cold storage.
DECLARE @t datetime2 = SYSDATETIME();
EXEC dbo.usp_SalesOrdersOffloadToCold @t;

-- Read hot plus cold data from the view.
SELECT * FROM dbo.SalesOrders;
GO

-- Again, retrieve the name of every partition.
-- The stored procedure can modify the partitions.
SELECT OBJECT_NAME( object_id) , partition_number , row_count
  FROM sys.dm_db_partition_stats ps
  WHERE object_id = OBJECT_ID( 'dbo.SalesOrders_cold')
    AND index_id = 1;
```

### <a name="drop-all-the-demo-objects"></a>捨棄所有示範物件

請記得將示範測試資料庫從測試系統中清除。

```sql
-- You must first leave the context of the PartitionSample database.

-- USE <A-Database-Name-Here>;
GO

DROP DATABASE PartitionSample;
GO
```

## <a name="see-also"></a>另請參閱

[記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)
