---
title: MERGE 函數 - 原生編譯的預存程序
ms.custom: seo-dt-2019
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: d4bcdc36-3302-4abc-9b35-64ec2b920986
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 811b3dfbd79e60d5fb626f814f7b4bf38272fd19
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412638"
---
# <a name="implementing-merge-functionality-in-a-natively-compiled-stored-procedure"></a>在原生編譯的預存程序中實作 MERGE 功能
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
本節中的 Transact-SQL 程式碼範例示範如何模擬原生編譯模組中的 T-SQL MERGE 陳述式。 此範例使用含識別資料行的資料表變數、逐一查看資料表變數中的資料列，並且在條件相符時針對每個資料列執行更新，並在條件不符時執行插入。
  
以下是原生程序內您要支援的 T-SQL MERGE 陳述式，以及程式碼範例所模擬的 T-SQL MERGE 陳述式。  
  
  
  
  
    MERGE INTO dbo.Table1 t  
        USING @tvp v  
        ON t.Column1 = v.c1  
        WHEN MATCHED THEN   
            UPDATE SET Column2 = v.c2  
        WHEN NOT MATCHED THEN  
            INSERT (Column1, Column2) VALUES (v.c1, v.c2);  
  
  
  
  
以下 T-SQL 可達成此因應措施，並模擬 MERGE。  
  
  
  
  
    DROP PROCEDURE IF EXISTS dbo.usp_merge1;  
    go  
    DROP TYPE IF EXISTS dbo.Type1;  
    go  
    DROP TABLE IF EXISTS dbo.Table1;  
    go  
    -----------------------------  
    -- target table and table type used for the workaround
    -----------------------------  
  
    CREATE TABLE dbo.Table1  
    (  
        Column1  INT  NOT NULL  PRIMARY KEY NONCLUSTERED,  
        Column2  INT  NOT NULL  
    )   
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
  
    CREATE TYPE dbo.Type1 AS TABLE  
    (  
        c1  INT  NOT NULL,  
        c2  INT  NOT NULL,  
  
        RowID    INT  NOT NULL  IDENTITY(1,1),  
        INDEX ix_RowID HASH (RowID) WITH (BUCKET_COUNT=1024)  
    )   
        WITH (MEMORY_OPTIMIZED = ON);  
    go  
    -----------------------------  
    -- stored procedure implementing the workaround
    -----------------------------  
  
    CREATE PROCEDURE dbo.usp_merge1   
        @tvp1 dbo.Type1 READONLY  
        WITH  
        NATIVE_COMPILATION, SCHEMABINDING  
    AS   
    BEGIN ATOMIC  
        WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
              LANGUAGE = N'us_english')  

        DECLARE  @i INT = 1,  @c1 INT,  @c2 INT;  
    
        WHILE @i > 0  
        BEGIN  
            SELECT @c1 = c1, @c2 = c2  
                FROM @tvp1  
                WHERE RowID = @i;  
    
            --test whether the row exists in the TVP; if not, we end the loop
            IF @@ROWCOUNT=0  
                SET @i = 0
            ELSE
            BEGIN
                -- try the update
                UPDATE dbo.Table1  
                    SET   Column2 = @c2  
                    WHERE Column1 = @c1;  
    
                -- if there was no row to update, we insert
                IF @@ROWCOUNT=0  
                    INSERT INTO dbo.Table1 (Column1, Column2)  
                        VALUES (@c1, @c2);  
    
                SET @i += 1
            END
        END  
    END  
    go  
    -----------------------------  
    -- test to validate the functionality
    -----------------------------  
  
    INSERT dbo.Table1 VALUES (1,2);  
    go  
  
    SELECT N'Before-MERGE' AS [Before-MERGE], Column1, Column2  
        FROM dbo.Table1;  
    go  
  
    DECLARE @tvp1 dbo.Type1;  
  
    INSERT @tvp1 (c1, c2) VALUES (1,33), (2,4);  
    EXECUTE dbo.usp_merge1 @tvp1;  
    go  
  
    SELECT N'After--MERGE' AS [After--MERGE], Column1, Column2  
        FROM dbo.Table1;  
    go  
    -----------------------------  

  
    /****  Actual output:  
  
    Before-MERGE   Column1   Column2  
    Before-MERGE      1         2  
  
    After--MERGE   Column1   Column2  
    After--MERGE      1        33  
    After--MERGE      2         4  
    ****/  
  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯預存程序的移轉問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [記憶體中的 OLTP 不支援 Transact-SQL 建構](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
