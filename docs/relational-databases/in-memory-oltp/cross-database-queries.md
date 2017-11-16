---
title: "跨資料庫查詢 | Microsoft Docs"
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 41b00b196f6cfad66ae0e26bbb1516da2641d9b7
ms.openlocfilehash: 8289b02c3e15f1b299196c343503c9cb87387c6c
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="cross-database-queries"></a>跨資料庫查詢
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  自 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]起，記憶體最佳化資料表不支援跨資料庫的交易。 您無法在同時存取記憶體最佳化資料表的相同交易或相同查詢中存取另一個資料庫。 您無法輕鬆地從某一個資料庫的資料表中，將資料複製到另一個資料庫中的記憶體最佳化資料表。  
  
 資料表變數並非交易式。 因此，記憶體最佳化資料表變數可以在跨資料庫查詢中使用，也因而有助於將某個資料庫中的資料移至另一個資料庫的記憶體最佳化資料表中。 您可以使用兩筆交易。 在第一筆交易中，將資料從遠端資料表插入變數中。 在第二筆交易中，從變數中將資料插入本機記憶體最佳化資料表。  如需記憶體最佳化資料表變數的詳細資訊，請參閱 [使用記憶體最佳化加快暫存資料表與資料表變數的速度](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)。
  
## <a name="example"></a>範例
本例說明將某個資料庫的資料傳送至不同資料庫的記憶體最佳化資料表的方法。

1. 建立測試物件。  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中執行下列 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  

    ```tsql

    USE master;
    GO
    
    SET NOCOUNT ON;
    
    -- Create simple database
    CREATE DATABASE SourceDatabase;
    ALTER DATABASE SourceDatabase SET RECOVERY SIMPLE;
    GO

    -- Create a table and insert a few records
    USE SourceDatabase;
    
    CREATE TABLE SourceDatabase.[dbo].[SourceTable] (
        [ID] [int] PRIMARY KEY CLUSTERED,
        [FirstName] nvarchar(8)
        );
    
    INSERT [SourceDatabase].[dbo].[SourceTable]
    VALUES (1, N'Bob'),
        (2, N'Susan');
    GO

    -- Create a database with a MEMORY_OPTIMIZED_DATA filegroup

    CREATE DATABASE DestinationDatabase
     ON  PRIMARY 
    ( NAME = N'DestinationDatabase_Data', FILENAME = N'D:\DATA\DestinationDatabase_Data.mdf',   SIZE = 8MB), 
     FILEGROUP [DestinationDatabase_mod] CONTAINS MEMORY_OPTIMIZED_DATA  DEFAULT
    ( NAME = N'DestinationDatabase_mod', FILENAME = N'D:\DATA\DestinationDatabase_mod', MAXSIZE = UNLIMITED)
     LOG ON 
    ( NAME = N'DestinationDatabase_Log', FILENAME = N'D:\LOG\DestinationDatabase_Log.ldf', SIZE = 8MB);
    
    ALTER DATABASE DestinationDatabase SET RECOVERY SIMPLE;
    GO
    
    USE DestinationDatabase;
    GO

    -- Create a memory-optimized table
    CREATE TABLE [dbo].[DestTable_InMem] (
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )
    WITH ( MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA );
    GO
    ```

2.  嘗試跨資料庫查詢。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中執行下列 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
  
    ```tsql  
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem]
    SELECT * FROM [SourceDatabase].[dbo].[SourceTable]
    ```  

    您應該會收到下列錯誤訊息：
    > 訊息 41317，層級 16，狀態 5  
    > 存取記憶體最佳化資料表或原生編譯模組的使用者交易，無法存取多位使用者資料庫或資料庫模型與 msdb，且不能寫入 master。

3.  建立記憶體最佳化資料表類型。  在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中執行下列 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。

    ```tsql
    USE DestinationDatabase;
    GO
    
    CREATE TYPE [dbo].[MemoryType]  
        AS TABLE  
        (  
        [ID] [int] PRIMARY KEY NONCLUSTERED,
        [FirstName] nvarchar(8)
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
    GO
    ```

4.  重新嘗試跨資料庫查詢。  這一次，來源資料會先傳送給記憶體最佳化資料表變數。  接著 table 變數的資料會傳輸至記憶體最佳化資料表。
    ```tsql
    -- Declare table variable utilizing the newly created type - MemoryType
    DECLARE @InMem dbo.MemoryType;
    
    -- Populate table variable
    INSERT @InMem SELECT * FROM SourceDatabase.[dbo].[SourceTable];
    
    -- Populate the destination memory-optimized table
    INSERT [DestinationDatabase].[dbo].[DestTable_InMem] SELECT * FROM @InMem;
    GO 
    ```
   
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  

