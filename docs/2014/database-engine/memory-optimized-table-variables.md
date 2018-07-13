---
title: 記憶體最佳化資料表變數 |Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bd102e95-53e2-4da6-9b8b-0e4f02d286d3
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1ec91cf243fbaa131ca85e7585e448ddb93f36f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157069"
---
# <a name="memory-optimized-table-variables"></a>記憶體最佳化資料表變數
  此外，（提供有效率的資料存取） 的記憶體最佳化資料表和原生編譯預存程序 （提供高效率的查詢處理和商務邏輯執行）[!INCLUDE[hek_2](../includes/hek-2-md.md)]導入了第三種物件： 記憶體最佳化資料表類型。 使用記憶體最佳化資料表類型建立的資料表變數，就是記憶體最佳化資料表變數。  
  
 與磁碟資料表變數相較之下，記憶體最佳化資料表變數提供了下列幾項優點：  
  
-   變數只儲存在記憶體中。 資料存取將更有效率，因為記憶體最佳化資料表類型使用的記憶體最佳化演算法和資料結構，與記憶體最佳化資料表所使用的相同，特別是在原生編譯預存程序中使用變數時。  
  
-   有了記憶體最佳化資料表變數，就不會使用 tempdb。 資料表變數不會儲存在 tempdb 中，而且不會使用 tempdb 中的任何資源。  
  
 記憶體最佳化資料表變數的一般使用案例包括：  
  
-   根據原生編譯預存程序中的多個查詢儲存中繼結果並建立單一結果集。  
  
-   將資料表值參數傳遞至原生編譯預存程序和解譯的預存程序中。  
  
-   取代磁碟資料表變數，以及在某些情況下取代預存程序的本機 #temp 資料表。 如果系統中有大量 tempdb 競爭，這就會特別有用。  
  
-   資料表變數可用來模擬以原生方式編譯之預存程序中的資料指標，這樣可協助您在以原生方式編譯的預存程序中避開介面區限制。  
  
 就像記憶體最佳化的資料表，一樣[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]會產生每個記憶體最佳化資料表類型的 DLL。 (編譯作業會在記憶體最佳化資料表類型建立時叫用，而不會在用來建立記憶體最佳化資料表變數時叫用)。此 DLL 包括存取索引以及從資料表變數擷取資料的函數。 根據資料表類型宣告記憶體最佳化資料表變數時，會在使用者工作階段中建立對應至資料表類型之資料表和索引結構的執行個體。 接著就可以透過與磁碟資料表變數相同的方式使用資料表變數。 您可以在資料表變數中插入、更新及刪除資料列，也可以在 [!INCLUDE[tsql](../includes/tsql-md.md)] 查詢中使用變數。 您也可以將變數當做資料表值參數 (TVP) 傳遞至以原生方式編譯和解譯的預存程序中。  
  
 下列範例將示範 AdventureWorks 為基礎的記憶體內部 OLTP 範例記憶體最佳化資料表類型 ([SQL Server 2014 記憶體中 OLTP 範例](https://msftdbprodsamples.codeplex.com/releases/view/114491))。  
  
```tsql
CREATE TYPE Sales.SalesOrderDetailType_inmem
   AS TABLE
(
   OrderQty         smallint   NOT NULL,
   ProductID        int        NOT NULL,

   SpecialOfferID   int        NOT NULL
      INDEX  IX_SpecialOfferID  NONCLUSTERED,

   LocalID          int        NOT NULL,

   INDEX IX_ProductID HASH (ProductID)
      WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```  
  
 此範例顯示，記憶體最佳化資料表類型的語法類似於磁碟資料表類型，但是有下列例外狀況：  
  
-   `MEMORY_OPTIMIZED=ON` 指出資料表類型為記憶體最佳化。  
  
-   類型必須至少有一個索引。 就像在記憶體最佳化資料表中，您可以使用雜湊和非叢集索引。  
  
     若是雜湊索引，值區計數應該約為預期的唯一索引鍵數目的一倍到兩倍。 如需詳細資訊，請參閱 <<c0> [ 判斷雜湊索引的正確貯體計數](../relational-databases/indexes/indexes.md)。  
  
-   對於記憶體最佳化資料表的資料類型和條件約束限制也適用於記憶體最佳化資料表類型。 例如，[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 支援預設條件約束，但是不支援檢查條件約束。  
  
 就像記憶體最佳化資料表，記憶體最佳化資料表變數  
  
-   不支援平行計畫。  
  
-   必須納入記憶體中，且不使用磁碟資源。  
  
 磁碟資料表變數存在於 tempdb 中。 記憶體最佳化資料表變數存在使用者資料庫中 (但是不會耗用儲存體，也不會復原)。  
  
 您無法使用內嵌語法建立記憶體最佳化資料表變數。 與磁碟資料表變數不同的是，您必須先建立類型。  
  
## <a name="table-valued-parameters"></a>資料表值參數  
 下列範例指令碼示範如何將資料表變數宣告為記憶體最佳化資料表類型 `Sales.SalesOrderDetailType_inmem`、將三個資料列插入變數中，以及將變數當做 TVP 傳遞至 `Sales.usp_InsertSalesOrder_inmem` 中。  
  
```tsql  
DECLARE @od Sales.SalesOrderDetailType_inmem,  
  @SalesOrderID uniqueidentifier,  
  @DueDate datetime2 = SYSDATETIME()  
  
INSERT @od (LocalID, ProductID, OrderQty, SpecialOfferID) VALUES  
  (1, 888, 2, 1),  
  (2, 450, 13, 1),  
  (3, 841, 1, 1)  
  
EXEC Sales.usp_InsertSalesOrder_inmem  
  @SalesOrderID = @SalesOrderID,  
  @DueDate = @DueDate,  
 @OnlineOrderFlag = 1,  
  @SalesOrderDetails = @od  
```  
  
 記憶體最佳化資料表類型可以做為預存程序資料表值參數 (TVP) 的類型使用，並且可以供用戶端參考，與磁碟資料表類型和 TVP 完全相同。 因此，採用記憶體最佳化 TVP 之預存程序和原生方式編譯之預存程序的引動過程，與採用磁碟 TVP 之解譯預存程序的引動過程完全相同。  
  
## <a name="temp-table-replacement"></a>取代 #temp 資料表  
 下列範例將示範記憶體最佳化資料表類型和資料表變數，做為預存程序之本機 #temp 資料表的替代方式。  
  
```tsql  
-- Using SQL procedure and temp table  
CREATE TABLE #tempTable (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
  
CREATE PROCEDURE sqlProc  
AS  
BEGIN  
  TRUNCATE TABLE #tempTable  
  
  INSERT #tempTable VALUES (1)  
  INSERT #tempTable VALUES (2)  
  INSERT #tempTable VALUES (3)  
  SELECT * FROM #tempTable  
END  
GO  
  
-- Using natively compiled stored procedure and table variable  
CREATE TYPE TT AS TABLE (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
GO  
  
CREATE PROCEDURE NCSPProc  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @tableVariable TT  
  INSERT @tableVariable VALUES (1)  
  INSERT @tableVariable VALUES (2)  
  INSERT @tableVariable VALUES (3)  
  SELECT c FROM @tableVariable  
END  
GO  
```  
  
## <a name="creating-a-single-result-set"></a>建立單一結果集  
 下列範例將示範如何根據原生編譯預存程序中的多個查詢儲存中繼結果並建立單一結果集。 此範例將計算聯集 `SELECT c1 FROM dbo.t1 UNION SELECT c1 FROM dbo.t2`。  
  
```tsql  
CREATE DATABASE hk  
GO  
ALTER DATABASE hk ADD FILEGROUP hk_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hk ADD FILE( NAME = 'hk_mod' , FILENAME = 'c:\data\hk_mod') TO FILEGROUP hk_mod;  
  
USE hk  
GO  
  
CREATE TYPE tab1 AS TABLE (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON)  
  
CREATE TABLE dbo.t1 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
CREATE TABLE dbo.t2 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
  
INSERT INTO dbo.t1 VALUES (1), (2)  
INSERT INTO dbo.t2 VALUES (3), (4)  
GO  
  
CREATE PROCEDURE dbo.p1  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS  
  BEGIN ATOMIC WITH ( TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english' )  
  
    DECLARE @t dbo.tab1  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t1;  
  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t2;  
  
    SELECT c1 FROM @t;  
  END  
GO  
  
EXEC dbo.p1  
GO  
```  
  
## <a name="memory-consumption-for-table-variables"></a>資料表變數的記憶體耗用量  
 資料表變數的記憶體耗用量類似於記憶體最佳化的資料表，但有非叢集索引的例外狀況。 如果您將大量資料列插入含有非叢集索引的記憶體最佳化資料表變數中，而且如果索引鍵很大，這些資料表變數將會使用不成比例的記憶體數量。 對於在資料表中插入相同數目的資料列而言，大型資料表變數上的非叢集索引比單一非叢集索引在比例上需要更多記憶體 (索引頁中需要更多記憶體)。  
  
 資料表變數的記憶體來自資料庫的資源管理員資源集區。  
  
 與記憶體最佳化的資料表不同，當資料表變數脫離範圍時，會釋出資料表變數所耗用的記憶體 (包括已刪除的資料列)。  
  
 屬於資料庫的單一 PGPOOL 記憶體取用者時，才會計算記憶體。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP 的 Transact-SQL 支援](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
