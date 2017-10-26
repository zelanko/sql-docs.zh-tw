---
title: "示範：記憶體內部 OLTP 的效能改善 | Microsoft 文件"
ms.custom: 
ms.date: 08/19/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6a6edd38b5efb5b617308b9359eea8d255daeb8d
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>示範：記憶體中 OLTP 的效能改善
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主題中的程式碼範例示範記憶體最佳化資料表的快速效能。 從傳統、解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)]存取記憶體最佳化資料表中的資料時，此效能改善顯而易見。 若從原生編譯的預存程序 (NCSProc) 存取記憶體最佳化資料表中的資料，則此效能改善的幅度甚至更高。  
 
若要查看記憶體中 OLTP 潛在效能改善的更完整示範，請參閱 [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)(記憶體中 OLTP 效能示範 1.0 版)。 
  
 現有文章中的程式碼範例為單一執行緒，且未利用記憶體內部 OLTP 的並行優點。 工作負載若是使用並行作業，將會有更高幅度的效能提升。 此程式碼範例僅示範某層面的效能改善 (即 INSERT 的資料存取效率)。  
  
 從 NCSProc 存取記憶體最佳化資料表中的資料時，可完全實現記憶體最佳化資料表所提供的效能改善。  
  
## <a name="code-example"></a>程式碼範例  
 下列小節將描述每個步驟。  
  
### <a name="step-1a-prerequisite-if-using-includessnoversionincludesssnoversion-mdmd"></a>步驟 1a︰使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 此第一個小節中的步驟僅適用於在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中執行時，但不適用於在 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]中執行時。 執行下列動作：  
  
1.  使用 SQL Server Management Studio (SSMS.exe) 連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 或者，任何與 SSMS.exe 類似的工具也可以。  
  
2.  手動建立名為 **C:\data\\** 的目錄。 範例 Transact-SQL 程式碼必須有預先存在的目錄。  
  
3.  執行簡短 T-SQL 來建立資料庫和其記憶體最佳化檔案群組。  
  
```tsql  
go  
CREATE DATABASE imoltp;    --  Transact-SQL  
go  
  
ALTER DATABASE imoltp ADD FILEGROUP [imoltp_mod]  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
ALTER DATABASE imoltp ADD FILE  
    (name = [imoltp_dir], filename= 'c:\data\imoltp_dir')  
    TO FILEGROUP imoltp_mod;  
go  
  
USE imoltp;  
go  
```  
  
### <a name="step-1b-prerequisite-if-using-includesssdsfullincludessssdsfull-mdmd"></a>步驟 1b︰使用 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
 這個小節僅適用於使用 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]時。 執行下列動作：  
  
1.  決定程式碼範例將使用的現有測試資料庫。  
  
2.  如果您決定建立新的測試資料庫，請使用 [Azure 入口網站](http://portal.azure.com) 來建立名為 **imoltp**的資料庫。  
  
 如果您想要使用 Azure 入口網站進行這項作業的指示，請參閱 [開始使用 Azure SQL Database](http://azure.microsoft.com/documentation/articles/sql-database-get-started)。  
  
### <a name="step-2-create-memory-optimized-tables-and-ncsproc"></a>步驟 2：建立記憶體最佳化資料表和 NCSProc  
 此步驟建立記憶體最佳化資料表和原生編譯的預存程序 (NCSProc)。 執行下列動作：  
  
1.  使用 SSMS.exe 連接至新的資料庫。  
  
2.  在資料庫中執行下列 T-SQL。  
  
```tsql  
go  
DROP PROCEDURE IF EXISTS ncsp;  
DROP TABLE IF EXISTS sql;  
DROP TABLE IF EXISTS hash_i;  
DROP TABLE IF EXISTS hash_c;  
go  
  
CREATE TABLE [dbo].[sql] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
);  
go  
  
CREATE TABLE [dbo].[hash_i] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE TABLE [dbo].[hash_c] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE PROCEDURE ncsp  
    @rowcount INT,  
    @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[hash_c] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
END;  
go  
```  
  
### <a name="step-3-run-the-code"></a>步驟 3︰執行程式碼  
 現在，您可以執行可示範記憶體最佳化資料表效能的查詢。 執行下列動作：  
  
1.  使用 SSMS.exe，在資料庫中執行下列 T-SQL。  
  
     忽略任何速度或此第一次執行所產生的其他效能資料。 第一次執行確保執行數個僅一次性作業 (例如初始配置記憶體)。  
  
2.  同樣地，使用 SSMS.exe，在資料庫中重新執行下列 T-SQL。  
  
```tsql  
go  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Inserts, one at a time.  
  
DECLARE @starttime DATETIME2 = sysdatetime();  
DECLARE @timems INT;  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
  
-- Harddrive-based table and interpreted Transact-SQL.  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[sql] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'A: Disk-based table and interpreted Transact-SQL: '  
    + cast(@timems AS VARCHAR(10)) + ' ms';  
  
-- Interop Hash.  
  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
    BEGIN;  
      INSERT INTO [dbo].[hash_i] VALUES (@i, @c);  
      SET @i += 1;  
    END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'B: memory-optimized table with hash index and interpreted Transact-SQL: '  
    + cast(@timems as VARCHAR(10)) + ' ms';  
  
-- Compiled Hash.  
  
SET @starttime = sysdatetime();  
  
EXECUTE ncsp @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'C: memory-optimized table with hash index and native SP:'  
    + cast(@timems as varchar(10)) + ' ms';  
go  
  
DELETE sql;  
DELETE hash_i;  
DELETE hash_c;  
go  
```  
  
 接下來是第二個測試執行所產生的輸出時間統計資料。  
  
```tsql  
10453 ms , A: Disk-based table and interpreted Transact-SQL.  
5626 ms , B: memory-optimized table with hash index and interpreted Transact-SQL.  
3937 ms , C: memory-optimized table with hash index and native SP.  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

