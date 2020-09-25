---
title: 記憶體最佳化資料表的查詢處理
description: 了解針對 SQL Server 中記憶體內部 OLTP 其記憶體最佳化資料表與原生編譯預存程序的查詢處理。
ms.custom: seo-dt-2019
ms.date: 05/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 065296fe-6711-4837-965e-252ef6c13a0f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed9bec3042903f22c4a4c71ac4f07520062e60c9
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90989901"
---
# <a name="a-guide-to-query-processing-for-memory-optimized-tables"></a>記憶體最佳化資料表的查詢處理指南
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  記憶體中 OLTP 推出記憶體最佳化資料表以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的原生編譯預存程序。 本文針對記憶體最佳化資料表和原生編譯的預存程序提供查詢處理的概觀。  
  
 本文件說明如何編譯和執行記憶體最佳化資料表上的查詢，包含：  
  
-   對於磁碟基礎的資料表， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的查詢處理管線。  
  
-   查詢最佳化；統計資料在記憶體最佳化資料表上的角色，以及對不正確的查詢計劃進行疑難排解的方針。  
  
-   使用解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 以存取記憶體最佳化資料表。  
  
-   有關記憶體最佳化資料表存取之查詢最佳化的考量。  
  
-   原生編譯預存程序編譯和處理。  
  
-   最佳化工具用於估計成本的統計資料。  
  
-   修正不正確查詢計劃的方式。  
  
## <a name="example-query"></a>範例查詢  
 下列範例將用來說明本文中所討論的查詢處理概念。  
  
 我們假設兩個資料表 Customer 和 Order。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼包含這兩個資料表與相關聯索引的定義 (以磁碟為基礎 (傳統) 的格式)：  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY,  
  ContactName nvarchar (30) NOT NULL   
)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY,  
  CustomerID nchar (5) NOT NULL,  
  OrderDate date NOT NULL  
)  
GO  
CREATE INDEX IX_CustomerID ON dbo.[Order](CustomerID)  
GO  
CREATE INDEX IX_OrderDate ON dbo.[Order](OrderDate)  
GO  
```  
  
 為了建構本文中所顯示的查詢計劃，這兩個資料表中已填入 Northwind 範例資料庫中的範例資料，您可以從 [Northwind and pubs Sample Databases for SQL Server 2000](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)(SQL Server 2000 的 Northwind 和 pubs 範例資料庫) 下載該資料庫。  
  
 請看下列查詢，其中聯結了 Customer 和 Order 這兩個資料表，並且會傳回訂單識別碼和相關聯的客戶資訊：  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 執行計畫大致如下面的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 所示  
  
 ![聯結磁碟為基礎資料表的查詢計劃。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-1.png "聯結磁碟為基礎資料表的查詢計劃。")  
聯結磁碟為基礎資料表的查詢計劃。  
  
 關於這個查詢計劃：  
  
-   Customer 資料表中的資料列是從叢集索引擷取，這是主要資料結構且擁有完整的資料表資料。  
  
-   來自 Order 資料表的資料，使用 CustomerID 資料行上的非叢集索引擷取得來。 這個索引同時包含用於聯結的 CustomerID 資料行，以及傳回給使用者的主索引鍵資料行 OrderID。 從 Orders 資料表傳回其他資料行會需要查閱 Order 資料表的叢集索引。  
  
-   邏輯運算子 **Inner Join** 是由實體運算子 **Merge Join**所實作。 其他實體聯結類型包括 **Nested Loops** 和 **Hash Join**。 **Merge Join** 運算子會利用兩個索引都會在聯結資料行 CustomerID 上排序的情況。  
  
 請考慮與這個查詢稍微不同的做法，傳回 Order 資料表的所有資料列，而不只是 OrderID：  
  
```sql  
SELECT o.*, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 這個查詢的計畫大致如下：  
  
 ![磁碟為基礎資料表的雜湊聯結查詢計劃。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-2.png "磁碟為基礎資料表的雜湊聯結查詢計劃。")  
磁碟為基礎資料表的雜湊聯結查詢計劃。  
  
 在這個查詢中，Orders 資料表的資料列是使用叢集索引擷取。 **Hash Match** 實體運算子現在用於 **Inner Join**。 Order 上的叢集索引不會在 CustomerID 上排序，因此 **Merge Join** 會需要排序運算子，而這樣就會影響效能。 請記下與上一個範例中 **Merge Join** 運算子成本 (46%) 相較的 **Hash Match** 運算子相對成本 (75%)。 最佳化工具原本也會在上一個範例中考慮 **Hash Match** 運算子，但結果卻是 **Merge Join** 運算子提供更佳效能的結果。  
  
## <a name="ssnoversion-query-processing-for-disk-based-tables"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁碟資料表的查詢處理  
 下圖概述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中隨選查詢的查詢處理流程：  
  
 ![SQL Server 查詢處理管線。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-3.png "SQL Server 查詢處理管線。")  
SQL Server 查詢處理管線。  
  
 在此情節中：  
  
1.  使用者會發出查詢。  
  
2.  剖析器和 Algebrizer 會利用根據使用者所提交 [!INCLUDE[tsql](../../includes/tsql-md.md)] 文字的邏輯運算子建構查詢樹狀結構。  
  
3.  最佳化工具會建立包含實體運算子 (例如，巢狀迴圈聯結) 的最佳化查詢計劃。 在最佳化之後，計畫可能會儲存到計畫快取中。 如果計畫快取中已包含這個查詢的計畫，則會略過這個步驟。  
  
4.  查詢執行引擎會處理查詢計劃的解譯。  
  
5.  對於每個索引搜尋、索引掃描和資料表掃描運算子，執行引擎都會向 Access Methods 的個別索引和資料表結構要求資料列。  
  
6.  Access Methods 會從緩衝集區中的索引和資料頁面擷取資料列，並且視需要將頁面從磁碟載入至緩衝集區。  

 在第一個範例查詢中，執行引擎會從 Access Methods 要求 Customer 上叢集索引中的資料列，以及 Order 上非叢集索引中的資料列。 Access Methods 會周遊 B 型樹狀目錄索引結構，擷取所要求的資料列。 在這種情況下，當計畫需要完整索引掃描時，就會擷取所有資料列。  
  
## <a name="interpreted-tsql-access-to-memory-optimized-tables"></a>對記憶體最佳化資料表進行解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 隨選批次和預存程序，也稱為解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 解譯是指查詢計劃是由查詢計劃中每個運算子的查詢執行引擎所解譯。 執行引擎會讀取運算子及其參數，並執行作業。  
  
 解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可用來存取記憶體最佳化和磁碟為基礎的資料表。 下圖說明對記憶體最佳化資料表進行解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取之查詢處理：  
  
 ![用於解譯之 tsql 的查詢處理管線。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-4.png "用於解譯 TSQL 的查詢處理管道。")  
對記憶體最佳化資料表進行解譯的 Transact-SQL 存取之查詢處理管線。  
  
 如圖中所示，查詢處理管線大致保持不變：  
  
-   剖析器和 Algebrizer 會建構查詢樹狀結構。  
  
-   最佳化工具會建立執行計畫。  
  
-   查詢執行引擎會解譯執行計畫。  
  
 與傳統查詢處理管線的主要差異 (圖 2) 在於，記憶體最佳化資料表的資料列不是使用 Access Methods 從緩衝集區擷取，資料列反而是透過記憶體中 OLTP 引擎從記憶體中的資料結構擷取。 資料列是透過記憶體中 OLTP 引擎從記憶體中的資料結構擷取。 資料結構的差異造成最佳化工具在某些情況下挑選不同的計畫，如下面範例所示。  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼包含 Order 和 Customer 資料表的記憶體最佳化版本 (使用雜湊索引)：  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY NONCLUSTERED,  
  ContactName nvarchar (30) NOT NULL   
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY NONCLUSTERED,  
  CustomerID nchar (5) NOT NULL INDEX IX_CustomerID HASH(CustomerID) WITH (BUCKET_COUNT=100000),  
  OrderDate date NOT NULL INDEX IX_OrderDate HASH(OrderDate) WITH (BUCKET_COUNT=100000)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
```  
  
 請考慮在記憶體最佳化的資料表上執行相同的查詢：  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 估計的計畫如下所示：  
  
 ![聯結記憶體最佳化資料表的查詢計劃。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-5.png "聯結記憶體最佳化資料表的查詢計劃。")  
聯結記憶體最佳化資料表的查詢計劃。  
  
 請觀察與磁碟為基礎的資料表 (圖 1) 上相同查詢的下列差異：  
  
-   這個計畫針對 Customer 資料表適用的資料表掃描，而非叢集索引掃描：  
  
    -   資料表定義不包含叢集索引。  
  
    -   記憶體最佳化資料表不支援叢集索引。 不過，每個記憶體最佳化的資料表都必須至少有一個非叢集索引，而且記憶體最佳化資料表上的所有索引均可有效率地存取資料表中的所有資料行，不必將資料行儲存於索引中，或參考叢集的索引。  
  
-   這個計畫包含 **Hash Match** ，而不是 **Merge Join**。 Order 和 Customer 資料表上的索引是雜湊索引，因此未進行排序。 **Merge Join** 會需要排序運算子，而這樣會降低效能。  
  
## <a name="natively-compiled-stored-procedures"></a>原生編譯的預存程序  
 原生編譯的預存程序是編譯成機器碼的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序，而不是由查詢執行引擎所解譯。 下列指令碼會建立執行範例查詢的原生編譯預存程序 (從「範例查詢」區段)。  
  
```sql  
CREATE PROCEDURE usp_SampleJoin  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = 'english')  
  
  SELECT o.OrderID, c.CustomerID, c.ContactName   
FROM dbo.[Order] o INNER JOIN dbo.[Customer] c   
  ON c.CustomerID = o.CustomerID  
  
END  
```  
  
 原生編譯的預存程序會在建立時編譯，而解譯的預存程序則是在第一次執行時編譯 (編譯的一部分，尤其是指剖析和 Algebrization，會在建立時發生。 不過，對於解譯的預存程序，查詢計劃的最佳化是在第一次執行時進行)。重新編譯邏輯也很類似。 如果伺服器重新啟動，原生編譯的預存程序就會在第一次執行程序時重新編譯。 如果計畫已不在計畫快取中，解譯的預存程序就會重新編譯。 下表摘要說明原生編譯的預存程序及解譯的預存程序之編譯和重新編譯案例：  
  
|編譯類型|原生編譯|對記憶體最佳化資料表進行解譯的|  
|-|-----------------------|-----------------|  
|初始編譯|建立時。|第一次執行時。|  
|自動重新編譯|在資料庫或伺服器重新啟動之後，第一次執行程序時。|伺服器重新啟動時。 或者，從計畫快取收回，通常是依據結構描述或統計資料變更，或是記憶體壓力。|  
|手動重新編譯|使用 **sp_recompile**。|使用 **sp_recompile**。 您可以從快取手動收回計畫，例如透過 DBCC FREEPROCCACHE。 您也可以建立預存程序 WITH RECOMPILE，而該預存程序將在每次執行時重新編譯。|  
  
### <a name="compilation-and-query-processing"></a>編譯和查詢處理  
 下圖說明原生編譯預存程序的編譯程序：  
  
 ![預存程序的原生編譯。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-6.png "預存程序的原生編譯。")  
預存程序的原生編譯。  
  
 這個程序描述為：  
  
1.  使用者對 **發出** CREATE PROCEDURE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]陳述式。  
  
2.  剖析器和 Algebrizer 會為程序建立處理流程，以及為預存程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢建立樹狀結構。  
  
3.  最佳化工具會為預存程序中的所有查詢建立最佳化的查詢執行計畫。  
  
4.  記憶體中 OLTP 編譯器會採用具有內嵌最佳化查詢計劃的處理流程，並產生包含執行預存程序之機器碼的 DLL。  
  
5.  產生的 DLL 會載入記憶體中。  
  
 原生編譯預存程序的引動過程會轉譯為在 DLL 中呼叫函數。  
  
 ![執行原生編譯預存程序。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-7.png "執行原生編譯預存程序。")  
執行原生編譯預存程序。  
  
 原生編譯預存程序的引動過程描述如下：  
  
1.  使用者發出 **EXEC** _usp_myproc_ 陳述式。  
  
2.  剖析器會擷取名稱和預存程序參數。  
  
     如果陳述式已備妥，例如使用 **sp_prep_exec**，則剖析器不需要在執行時擷取程序名稱和參數。  
  
3.  記憶體中 OLTP 執行階段會尋找預存程序的 DLL 進入點。  
  
4.  然後會執行 DLL 中的機器碼，再將其結果傳回用戶端。  
  
 **參數探測**  
  
 與在建立時編譯的原生編譯預存程序相反，解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序會在第一次執行時編譯。 在引動過程中編譯解譯的預存程序時，最佳化工具會在產生執行計畫時使用提供給這個引動過程的參數值。 在編譯期間使用參數的動作，就稱為參數探測。  
  
 參數探測不會用於編譯原生編譯的預存程序。 預存程序的所有參數都會視為具有 UNKNOWN 值。 與解譯的預存程序相同，原生編譯的預存程序也支援 **OPTIMIZE FOR** 提示。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
### <a name="retrieving-a-query-execution-plan-for-natively-compiled-stored-procedures"></a>擷取原生編譯預存程序的查詢執行計畫  
 原生編譯預存程序的查詢執行計畫，可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的 [Estimated Execution Plan (估計的執行計畫)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的 SHOWPLAN_XML 選項加以擷取。 例如：  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC dbo.usp_myproc  
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 查詢最佳化工具所產生的執行計畫包含查詢運算子做為節點的樹狀結構，以及樹狀結構的分葉。 樹狀結構的結構決定運算子之間的互動 (資料列從一個運算子到另一個運算子的流程)。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的圖形檢視中，流程是由右至左。 例如，圖 1 中的查詢計劃包含兩個索引掃描運算子，這兩個運算子會提供資料列給合併聯結運算子。 合併聯結運算子會將資料列提供給選取運算子。 最後，選取運算子會將資料列傳回用戶端。  
  
### <a name="query-operators-in-natively-compiled-stored-procedures"></a>原生編譯預存程序中的查詢運算子  
 下表摘要說明原生編譯預存程序內部支援的查詢運算子：  
  
|運算子|範例查詢|注意|  
|--------------|------------------|-----------|  
|SELECT|`SELECT OrderID FROM dbo.[Order]`||  
|Insert|`INSERT dbo.Customer VALUES ('abc', 'def')`||  
|UPDATE|`UPDATE dbo.Customer SET ContactName='ghi' WHERE CustomerID='abc'`||  
|刪除|`DELETE dbo.Customer WHERE CustomerID='abc'`||  
|Compute Scalar|`SELECT OrderID+1 FROM dbo.[Order]`|這個運算子同時用於內建函數和類型轉換。 並非所有函數和類型轉換都可在原生編譯預存程序內部受到支援。|  
|Nested Loops Join|`SELECT o.OrderID, c.CustomerID FROM dbo.[Order] o INNER JOIN dbo.[Customer] c`|巢狀迴圈是原生編譯預存程序中唯一支援的聯結運算子。 即使做為解譯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 執行的相同查詢計劃包含雜湊或合併聯結，所有包含聯結的計畫還是都會使用 Nested Loops 運算子。|  
|Sort|`SELECT ContactName FROM dbo.Customer ORDER BY ContactName`||  
|頂端|`SELECT TOP 10 ContactName FROM dbo.Customer`||  
|Top-sort|`SELECT TOP 10 ContactName FROM dbo.Customer  ORDER BY ContactName`|**TOP** 運算式 (要傳回的資料列數目) 不得超過 8,000 個資料列。 如果查詢中也有聯結和彙總運算子，則數目會更少。 與基底資料表的資料列數相比，聯結和彙總運算子通常會減少要排序的資料列數。|  
|Stream Aggregate|`SELECT count(CustomerID) FROM dbo.Customer`|請注意，Hash Match 運算子不支援彙總。 因此，即使解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中相同查詢的計畫使用 Hash Match 運算子，原生編譯預存程序中的所有彙總仍會使用 Stream Aggregate 運算子。|  
  
## <a name="column-statistics-and-joins"></a>資料行統計資料和聯結  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在索引鍵資料行中維護值的統計資料，以協助估計特定作業的成本，例如索引掃描或索引搜尋。 (如果您明確建立非索引之索引鍵資料行的統計資料，或如果查詢最佳化工具為了回應包含述詞的查詢而建立它們，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也會建立這些統計資料。)成本估計的主要標準是單一運算子所處理的資料列數 請注意，對於磁碟基礎的資料表，特定運算子所存取的頁面數目在成本估計中佔有相當大的比例。 但是，由於頁面數對於記憶體最佳化資料表而言並不重要 (一律為零)，因此這裡的討論將著重在資料列計數。 估計時間是從計劃中的索引搜尋和掃描運算子開始算起，然後延伸以納入其他運算子，像是聯結運算子。 聯結運算子所要處理的估計資料列數是以基礎索引、搜尋和掃描運算子的估計為依據。 若要對記憶體最佳化資料表進行解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取，您可以觀察實際執行計畫，了解計畫中運算子的估計資料列計數和實際資料列計數之間的差異。  
  
在圖 1 的範例中，  
  
- Customer 上叢集索引掃描的資料列估計為 91；實際為 91。  
- CustomerID 上非叢集索引掃描的資料列估計為 830；實際為 830。  
- Merge Join 運算子的資料列估計為 815；實際為 830。  
  
索引掃描的估計是正確的。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會維護磁碟資料表的資料列計數。 完整資料表和索引掃描的估計永遠正確，而聯結的估計也一樣相當正確。 聯結的估計同樣相當正確。  
  
如果這些估計改變，不同計畫替代方式的成本考量也會改變。 例如，如果聯結其中一端的估計資料列計數為 1，或只有少數資料列，則使用巢狀迴圈聯結成本較低。 請考慮以下查詢：  
  
```sql
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
刪除 `Customer` 資料表中除了一個資料列以外的所有資料列之後，會產生下列查詢計劃：  
  
![資料行統計資料和聯結。](../../relational-databases/in-memory-oltp/media/hekaton-query-plan-9.png "資料行統計資料和聯結。")  
  
關於這個查詢計畫：  
  
- Hash Match 已取代為 Nested Loops 實體聯結運算子。  
- 對 IX_CustomerID 的完整索引掃描已取代為索引搜尋。 這樣的結果會是掃描 5 個資料列，而不是完整索引掃描所需的 830 個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
