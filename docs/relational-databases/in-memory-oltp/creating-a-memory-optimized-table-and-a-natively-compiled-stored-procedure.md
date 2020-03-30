---
title: 記憶體最佳化資料表和原生編譯的預存程序
ms.custom: seo-dt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 48a9a0a3-930f-477b-bd0f-e82e77999ecc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6e8793d5fc14401cbe800604accc6642a424fbbe
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412738"
---
# <a name="creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure"></a>建立記憶體最佳化資料表和原生編譯的預存程序

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主題包含介紹記憶體中 OLTP 語法的範例。  

若要讓應用程式能夠使用記憶體中 OLTP，您需要完成下列工作：  

-   建立記憶體最佳化資料檔案群組並將容器加入至檔案群組。  
  
-   建立記憶體最佳化資料表及索引 如需詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。  
  
-   將資料載入資料記憶體最佳化資料表，並於載入資料之後及建立編譯的預存程序之前更新統計資料。 如需詳細資訊，請參閱 [記憶體最佳化資料表的統計資料](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md)。  
  
-   建立原生編譯的預存程序來存取記憶體最佳化資料表中的資料。 如需詳細資訊，請參閱 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)。 您也可以使用傳統的解譯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取記憶體最佳化資料表中的資料。  
  
-   視需要將現有資料表中的資料移轉至記憶體最佳化資料表。  

## <a name="background-on-in-memory-objects"></a>記憶體內部物件的背景

如需如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立記憶體最佳化資料表的資訊，請參閱 [SQL Server Management Studio 對記憶體內部 OLTP 的支援](../../relational-databases/in-memory-oltp/sql-server-management-studio-support-for-in-memory-oltp.md)。  

### <a name="natively-compiled-stored-procedures"></a>原生編譯的預存程序

原生編譯預存程序是編譯成機器碼且可存取記憶體最佳化資料表的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序。 原生編譯預存程序允許以有效率的方式執行預存程序中的查詢和商務邏輯。 如需有關原生編譯程序的詳細資料，請參閱＜ [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md)＞。 如需將以磁碟為基礎之預存程序移轉至原生編譯預存程序的詳細資訊，請參閱 [原生編譯預存程序的移轉問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)。

> [!NOTE]
> 解譯 (以磁碟為基礎) 的預存程序與原生編譯的預存程序之間的差異在於，解譯的預存程序是在第一次執行時編譯，而原生編譯的預存程序是在建立時編譯。 原生編譯的預存程序於建立時將能偵測出許多錯誤狀況，而這會造成原生編譯的預存程序建立失敗 (例如算術溢位、類型轉換和一些除以零的狀況)。 若是解譯的預存程序，這些錯誤狀況通常不會導致預存程序建立失敗，但所有的執行都會失敗。

## <a name="code-example-in-t-sql"></a>T-SQL 程式碼範例

下列程式碼範例需要稱為 c:\Data\ 的目錄。

```sql  
CREATE DATABASE imoltp   
GO  
  
--------------------------------------  
-- create database with a memory-optimized
-- filegroup and a container.

ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE imoltp ADD FILE (
    name='imoltp_mod1', filename='c:\data\imoltp_mod1')
    TO FILEGROUP imoltp_mod;

ALTER DATABASE imoltp
    SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
GO  
  
USE imoltp  
GO  
  
-- Create a durable (data will be persisted) memory-optimized table
-- two of the columns are indexed.

CREATE TABLE dbo.ShoppingCart (   
    ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,  
    UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED
        HASH WITH (BUCKET_COUNT=1000000),
    CreatedDate DATETIME2 NOT NULL,   
    TotalPrice MONEY  
    ) WITH (MEMORY_OPTIMIZED=ON)   
GO  

-- Create a non-durable table. Data will not be persisted,
-- data loss if the server turns off unexpectedly.

CREATE TABLE dbo.UserSession (   
   SessionId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED
        HASH WITH (BUCKET_COUNT=400000),
   UserId int NOT NULL,   
   CreatedDate DATETIME2 NOT NULL,  
   ShoppingCartId INT,  
   INDEX ix_UserId NONCLUSTERED
        HASH (UserId) WITH (BUCKET_COUNT=400000)   
    )   
    WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_ONLY)
GO  
  
-- insert data into the tables  
INSERT dbo.UserSession VALUES (342, SYSDATETIME(), 4);
INSERT dbo.UserSession VALUES (65, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8798, SYSDATETIME(), 1)   
INSERT dbo.UserSession VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (4321, SYSDATETIME(), NULL)   
INSERT dbo.UserSession VALUES (8578, SYSDATETIME(), NULL)   
  
INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4)   
INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL)   
INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4)   
GO  
  
-- Verify table contents.

SELECT * FROM dbo.UserSession;
SELECT * FROM dbo.ShoppingCart;
GO  
  
-- Update statistics on memory-optimized tables;

UPDATE STATISTICS dbo.UserSession  WITH FULLSCAN, NORECOMPUTE;
UPDATE STATISTICS dbo.ShoppingCart WITH FULLSCAN, NORECOMPUTE;
GO  
  
-- in an explicit transaction, assign a cart to a session
-- and update the total price.
-- SELECT/UPDATE/DELETE statements in explicit transactions.

BEGIN TRAN;
   UPDATE dbo.UserSession SET ShoppingCartId=3 WHERE SessionId=4;
   UPDATE dbo.ShoppingCart SET TotalPrice=65.84 WHERE ShoppingCartId=3;
COMMIT;
GO   
  
-- Verify table contents.

SELECT *   
    FROM dbo.UserSession u
        JOIN dbo.ShoppingCart s on u.ShoppingCartId=s.ShoppingCartId
    WHERE u.SessionId=4;
 GO  
  
-- Natively compiled stored procedure for assigning
-- a shopping cart to a session.

CREATE PROCEDURE dbo.usp_AssignCart @SessionId int
    WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC
    WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
        LANGUAGE = N'us_english');
  
  DECLARE @UserId INT,  
          @ShoppingCartId INT;
  
  SELECT @UserId=UserId, @ShoppingCartId=ShoppingCartId
  FROM dbo.UserSession WHERE SessionId=@SessionId;
  
  IF @UserId IS NULL   
    THROW 51000, N'The session or shopping cart does not exist.', 1;
  
  UPDATE dbo.UserSession
    SET ShoppingCartId=@ShoppingCartId WHERE SessionId=@SessionId;
 END   
 GO  
  
 EXEC usp_AssignCart 1;
 GO  
  
-- natively compiled stored procedure for inserting
-- a large number of rows this demonstrates the
-- performance of native procs   
CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int
    WITH NATIVE_COMPILATION, SCHEMABINDING   
AS
BEGIN ATOMIC   
    WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
        LANGUAGE = N'us_english');
  
  DECLARE @i int = 0;
  
  WHILE @i < @InsertCount   
  BEGIN   
    INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL)
    SET @i += 1   
  END  
  
END   
GO  
  
-- insert 1,000,000 rows   
 EXEC usp_InsertSampleCarts 1000000   
 GO  
  
---- verify the rows have been inserted   
 SELECT COUNT(*) FROM dbo.ShoppingCart   
 GO  
  
-- Sample memory-optimized tables for
-- sales orders and sales order details.
CREATE TABLE dbo.SalesOrders   
(  
   so_id INT NOT NULL PRIMARY KEY NONCLUSTERED,  
   cust_id INT NOT NULL,  
   so_date DATE NOT NULL INDEX ix_date NONCLUSTERED,  
   so_total MONEY NOT NULL,  
   INDEX ix_date_total NONCLUSTERED
        (so_date DESC, so_total DESC)  
) WITH (MEMORY_OPTIMIZED=ON);
GO  
  
CREATE TABLE dbo.SalesOrderDetails  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   CONSTRAINT PK_SOD PRIMARY KEY NONCLUSTERED
        (so_id,lineitem_id)
) WITH (MEMORY_OPTIMIZED=ON)  
GO  

-- Memory-optimized table type for collecting
-- sales order details.

CREATE TYPE dbo.SalesOrderDetailsType AS TABLE  
(  
   so_id INT NOT NULL,  
   lineitem_id INT NOT NULL,  
   product_id INT NOT NULL,  
   unitprice MONEY NOT NULL,  
  
   PRIMARY KEY NONCLUSTERED (so_id,lineitem_id)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- stored procedure that inserts a sales order,
-- along with its details.

CREATE PROCEDURE dbo.InsertSalesOrder
    @so_id INT, @cust_id INT,
    @items dbo.SalesOrderDetailsType READONLY  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH   
(  
   TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
   LANGUAGE = N'us_english'  
)  
   DECLARE @total MONEY  
   SELECT @total = SUM(unitprice) FROM @items  

   INSERT dbo.SalesOrders
        VALUES (@so_id, @cust_id, getdate(), @total)

   INSERT dbo.SalesOrderDetails
        SELECT so_id, lineitem_id, product_id, unitprice
        FROM @items  
END  
GO  
  
-- Insert a sample sales order.
DECLARE @so_id INT = 18,  
       @cust_id INT = 8,  
       @items dbo.SalesOrderDetailsType;

INSERT @items  VALUES   
       (@so_id, 1, 4, 43),   
       (@so_id, 2, 3, 3),   
       (@so_id, 3, 8, 453),   
       (@so_id, 4, 5, 76),   
       (@so_id, 5, 4, 43);

EXEC dbo.InsertSalesOrder @so_id, @cust_id, @items;
GO  
  
-- verify the content of the tables  
SELECT   
       so.so_id,  
       so.so_date,  
       sod.lineitem_id,  
       sod.product_id,  
       sod.unitprice  
FROM dbo.SalesOrders so
    JOIN dbo.SalesOrderDetails sod on so.so_id=sod.so_id  
ORDER BY so.so_id, sod.lineitem_id  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP 程式碼範例](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)  
  
  
