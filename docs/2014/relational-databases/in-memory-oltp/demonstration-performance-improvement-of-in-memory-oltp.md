---
title: 示範：記憶體內部 OLTP 的效能改善 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c9477a318d2cb4f9886d67da8a4f8b5967cc180
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63071783"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>示範：記憶體中 OLTP 的效能改善
  此範例說明使用記憶體中 OLTP 時的效能改進，方法是比較對記憶體最佳化和傳統以磁碟為基礎的資料表執行相同的 Transact-SQL 查詢時，兩者的回應時間有何差異。 此外也會建立原生編譯的預存程序 (根據相同的查詢)，然後執行以示範您通常在使用原生編譯的預存程序來查詢記憶體最佳化資料表時，可獲得最佳的回應時間。 此範例僅顯示在記憶體最佳化資料表中存取資料時的其中一個效能改進層面；即執行插入時的資料存取效率。 此範例為單一執行緒且未利用記憶體中 OLTP 的並行優點。 工作負載若是使用並行作業，將會有更高幅度的效能提升。  
  
> [!NOTE]  
>  另一個示範記憶體最佳化資料表的範例可從 [SQL Server 2014 記憶體中 OLTP 範例](https://msftdbprodsamples.codeplex.com/releases/view/114491)取得。  
  
 若要完成此範例，您將執行下列作業：  
  
1.  建立名為 **imoltp** 的資料庫，並變更其檔案詳細資料，以便將它設定為使用記憶體中 OLTP。  
  
2.  建立範例的資料庫物件：三個資料表和原生編譯的預存程序。  
  
3.  執行不同的查詢，並顯示每個查詢的回應時間。  
  
 若要設定範例的 **imoltp** 資料庫，請先建立空的資料夾 **c:\imoltp_data**，然後執行下列程式碼：  
  
```sql  
USE master  
GO  
  
-- Create a new database.  
CREATE DATABASE imoltp  
GO  
  
-- Prepare the database for In-Memory OLTP by  
-- adding a memory-optimized filegroup to the database.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_file_group  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
-- Add a file (to hold the memory-optimized data) to the new filegroup.  
ALTER DATABASE imoltp ADD FILE (name='imoltp_file', filename='c:\imoltp_data\imoltp_file')  
    TO FILEGROUP imoltp_file_group;  
GO  
  
```  
  
 接下來，執行下列程式碼以建立以磁碟為基礎的資料表、兩個 (2) 記憶體最佳化資料表，和將用來示範不同資料存取方法的原生編譯預存程序：  
  
```sql  
USE imoltp  
GO  
  
-- If the tables or stored procedure already exist, drop them to start clean.  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'DiskBasedTable')  
   DROP TABLE [dbo].[DiskBasedTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'InMemTable')  
   DROP TABLE [dbo].[InMemTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'InMemTable2')  
   DROP TABLE [dbo].[InMemTable2]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'usp_InsertData')  
   DROP PROCEDURE [dbo].[usp_InsertData]  
GO  
  
-- Create a traditional disk-based table.  
CREATE TABLE [dbo].[DiskBasedTable] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
)  
GO  
  
-- Create a memory-optimized table.  
CREATE TABLE [dbo].[InMemTable] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a 2nd memory-optimized table.  
CREATE TABLE [dbo].[InMemTable2] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a natively-compiled stored procedure.  
CREATE PROCEDURE [dbo].[usp_InsertData]   
  @rowcount INT,  
  @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[inMemTable2](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
END  
GO  
  
```  
  
 設定完成後，我們即可執行查詢，以顯示回應時間來比較資料存取方法的效能。  
  
 若要完成範例，請執行下列程式碼多次。 請忽略第一次執行的結果，因為此結果受到初始記憶體配置的負面影響。  
  
```sql  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Delete data from all tables to reset the example.  
DELETE FROM [dbo].[DiskBasedTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[inMemTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[InMemTable2]   
    WHERE [c1]>0  
GO  
  
-- Declare parameters for the test queries.  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
DECLARE @timems INT;  
DECLARE @starttime datetime2 = sysdatetime();  
  
-- Disk-based table queried with interpreted Transact-SQL.  
BEGIN TRAN  
  WHILE @I <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[DiskBasedTable](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (disk-based table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with interpreted Transact-SQL.  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN  
  WHILE @i <= @rowcount  
    BEGIN  
      INSERT INTO [dbo].[InMemTable](c1,c2) VALUES (@i, @c);  
      SET @i += 1;  
    END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with a natively-compiled stored procedure.  
SET @starttime = sysdatetime();  
  
EXEC usp_InsertData @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with natively-compiled stored procedure).';  
  
```  
  
 預期的結果會提供實際的回應時間，顯示使用記憶體最佳化資料表和原生編譯的預存程序，為何通常在回應時間上都可優於針對傳統以磁碟為基礎的資料表執行相同的工作負載。  
  
## <a name="see-also"></a>另請參閱  
 [示範記憶體內部 OLTP 的 AdventureWorks 擴充功能](../../database-engine/extensions-to-adventureworks-to-demonstrate-in-memory-oltp.md)   
 [記憶體內部 OLTP &#40;記憶體內部優化&#41;](in-memory-oltp-in-memory-optimization.md)   
 [記憶體優化資料表](memory-optimized-tables.md)   
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)   
 [使用記憶體優化資料表的需求](requirements-for-using-memory-optimized-tables.md)   
 [建立資料庫 &#40;SQL Server Transact-sql&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [建立程式和記憶體優化資料表](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
