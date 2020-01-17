---
title: 記憶體最佳化加快暫存資料表與資料表變數的速度
ms.custom: seo-dt-2019
ms.date: 06/01/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 38512a22-7e63-436f-9c13-dde7cf5c2202
author: Jodebrui
ms.author: jodebrui
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 833108cfc5e8a11f72e8b7cb7b628690b0050c58
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412683"
---
# <a name="faster-temp-table-and-table-variable-by-using-memory-optimization"></a>使用記憶體最佳化加快暫存資料表與資料表變數的速度
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
如果您使用暫存資料表、資料表變數或資料表值參數，請考慮進行轉換，以便利用記憶體最佳化資料表和資料表變數來提升效能。 對程式碼所做的變更通常很少。  
  
本文章說明：  
  
- 有利於轉換成記憶體內部的案例。  
- 實作轉換成記憶體內部的技術性步驟。  
- 轉換成記憶體內部前的必要條件。  
- 強調記憶體最佳化之效能優點的程式碼範例
  
  
## <a name="a-basics-of-memory-optimized-table-variables"></a>A. 記憶體最佳化資料表變數的基本概念  
  
記憶體最佳化資料表變數使用記憶體最佳化資料表所使用的相同記憶體最佳化演算法和資料結構，來提供最佳效率。 當資料表變數從原生編譯模組內部存取時，其效率最高。  
  
  
記憶體最佳化資料表變數：  
  
- 只會儲存在記憶體中，在磁碟上沒有任何元件。  
- 不需要進行 IO 活動。  
- 不需要使用或競爭 tempdb。  
- 可傳入預存程序作為資料表值參數 (TVP)。  
- 至少必須有一個雜湊或非叢集索引。  
  - 若是雜湊索引，值區計數在理想情況下應該是預期唯一索引鍵數目的 1-2 倍，不過高估值區計數通常沒什麼問題 (最多 10 倍)。 如需詳細資訊，請參閱 [記憶體最佳化資料表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)。  

  
  
#### <a name="object-types"></a>物件類型  
  
記憶體內部 OLTP 提供可用於記憶體最佳化暫存資料表和資料表變數的下列物件：  
  
- 記憶體最佳化的資料表  
  - DURABILITY = SCHEMA_ONLY  
- 記憶體最佳化資料表變數  
  - 必須分兩個步驟 (而非內嵌) 宣告：  
    - `CREATE TYPE my_type AS TABLE ...;` ，則  
    - 第 1 課：建立 Windows Azure 儲存體物件`DECLARE @mytablevariable my_type;`。  
  
  
## <a name="b-scenario-replace-global-tempdb-x23x23table"></a>B. 案例：取代全域 tempdb &#x23;&#x23;table  
  
使用經記憶體最佳化的 SCHEMA_ONLY 資料表取代全域暫存資料表相當簡單。 最大的變更是在部署階段 (而非執行階段) 建立資料表。 因為編譯時間最佳化，所以建立經記憶體最佳化的資料表會花費比建立傳統資料表更長的時間。 在線上工作負載過程中建立和卸除經記憶體最佳化的資料表會影響工作負載的效能，也會影響 AlwaysOn 次要資料庫上的重做和資料庫復原的效能。

假設您有下列全域暫存資料表。  
  
  
```sql
CREATE TABLE ##tempGlobalB  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
```
  
  
  
請考慮使用 DURABILITY = SCHEMA_ONLY 的下列記憶體最佳化資料表，來取代全域暫存資料表。  
  
  
  
```sql
CREATE TABLE dbo.soGlobalB  
(  
    Column1   INT   NOT NULL   INDEX ix1 NONCLUSTERED,  
    Column2   NVARCHAR(4000)  
)  
    WITH  
        (MEMORY_OPTIMIZED = ON,  
        DURABILITY        = SCHEMA_ONLY);  
```  
  
  
  
#### <a name="b1-steps"></a>B.1 步驟  
  
從全域暫存轉換成 SCHEMA_ONLY 的步驟如下：  
  
  
1. 建立 **dbo.soGlobalB** 資料表一次，就像是任何傳統磁碟資料表一樣。  
2. 從 Transact-SQL 中移除建立的 **&#x23;&#x23;tempGlobalB** 資料表。  請務必在部署階段 (而非執行階段) 建立經記憶體最佳化的資料表，以避免因建立資料表而產生的編譯額外負荷。
3. 在 T-SQL 中，以 **dbo.soGlobalB** 取代所有提及的 **&#x23;&#x23;tempGlobalB**。  
  
  
## <a name="c-scenario-replace-session-tempdb-x23table"></a>C. 案例：取代工作階段 tempdb &#x23;table  
  
取代工作階段暫存資料表的準備工作，需要比先前的全域暫存資料表案例更多的 T-SQL。 幸好額外的 T-SQL 並不表示需要任何更多的工作才能完成轉換。  

如同全域暫存資料表案例，最大的變更是在部署階段 (而非執行階段) 建立資料表，以避免編譯額外負荷。
  
假設您有下列工作階段暫存資料表。  
  
  
  
```sql  
CREATE TABLE #tempSessionC  
(  
    Column1   INT   NOT NULL ,  
    Column2   NVARCHAR(4000)  
);  
```
  
  
  
第一步，建立下列資料表值函數，對 **\@\@spid** 進行篩選。 此函數將可供轉換自工作階段暫存資料表的所有 SCHEMA_ONLY 資料表使用。  
  
  
  
```sql  
CREATE FUNCTION dbo.fn_SpidFilter(@SpidFilter smallint)  
    RETURNS TABLE  
    WITH SCHEMABINDING , NATIVE_COMPILATION  
AS  
    RETURN  
        SELECT 1 AS fn_SpidFilter  
            WHERE @SpidFilter = @@spid;  
```
  
  
  
第二步，建立 SCHEMA_ONLY 資料表，以及資料表上的安全性原則。  
  
  
請注意，每個記憶體最佳化資料表至少必須有一個索引。  
  
- 針對資料表 dbo.soSessionC，如果我們計算出正確的 BUCKET_COUNT，雜湊索引可能更適合。 但針對本範例，我們將簡化為非叢集索引。  
  
  
  
```sql
CREATE TABLE dbo.soSessionC  
(  
    Column1     INT         NOT NULL,  
    Column2     NVARCHAR(4000)  NULL,  

    SpidFilter  SMALLINT    NOT NULL   DEFAULT (@@spid),  

    INDEX ix_SpidFiler NONCLUSTERED (SpidFilter),  
    --INDEX ix_SpidFilter HASH  
    --    (SpidFilter) WITH (BUCKET_COUNT = 64),  
        
    CONSTRAINT CHK_soSessionC_SpidFilter  
        CHECK ( SpidFilter = @@spid ),  
)  
    WITH  
        (MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_ONLY);  
go  
  
  
CREATE SECURITY POLICY dbo.soSessionC_SpidFilter_Policy  
    ADD FILTER PREDICATE dbo.fn_SpidFilter(SpidFilter)  
    ON dbo.soSessionC  
    WITH (STATE = ON);  
go  
```  
  
  
  
第三步，在您的一般 T-SQL 程式碼中：  
  
1. 將 Transact-SQL 陳述式中之暫存資料表的所有參考都變更為新的記憶體最佳化資料表︰
    - _舊名稱︰_ &#x23;tempSessionC  
    - _新名稱︰_ dbo.soSessionC  
2. 將程式碼中的 `CREATE TABLE #tempSessionC` 陳述式取代為 `DELETE FROM dbo.soSessionC`，以確保工作階段不會向前一個具有相同 session_id 的工作階段所插入的資料表內容公開。 請務必在部署階段 (而非執行階段) 建立經記憶體最佳化的資料表，以避免因建立資料表而產生的編譯額外負荷。
3. 從您的程式碼移除 `DROP TABLE #tempSessionC` 陳述式；如果記憶體大小是潛在問題，則也可以選擇性地插入 `DELETE FROM dbo.soSessionC` 陳述式
  
  
  
  
## <a name="d-scenario-table-variable-can-be-memory_optimizedon"></a>D. 案例：資料表變數可設為 MEMORY_OPTIMIZED=ON  
  
  
傳統資料表變數代表 tempdb 資料庫中的資料表。 如需更快的效能，您可以對資料表變數進行記憶體最佳化。  
  
以下是傳統資料表變數的 T-SQL。 其範圍結束於批次或工作階段結束時。  
  
  
  
```sql
DECLARE @tvTableD TABLE  
    ( Column1   INT   NOT NULL ,  
      Column2   CHAR(10) );  
```
  
  
  
#### <a name="d1-convert-inline-to-explicit"></a>D.1 將內嵌轉換成明確  
  
上述語法適用於建立資料表變數 *inline*。 此內嵌語法不支援記憶體最佳化。 因此請將 TYPE 的內嵌語法轉換成明確語法。  
  
範圍：  第一個 go 分隔之批次所建立的 TYPE 定義，即使在關閉並重新啟動伺服器之後仍然存在。 但在第一個 go 分隔符號之後，宣告的資料表 @tvTableC 只會保存至達到下一個 go 且批次結束時。  
  
  
  
```sql  
CREATE TYPE dbo.typeTableD  
    AS TABLE  
    (  
        Column1  INT   NOT NULL ,  
        Column2  CHAR(10)  
    );  
go  
        
SET NoCount ON;  
DECLARE @tvTableD dbo.typeTableD  
;  
INSERT INTO @tvTableD (Column1) values (1), (2)  
;  
SELECT * from @tvTableD;  
go  
```
  
  
  
#### <a name="d2-convert-explicit-on-disk-to-memory-optimized"></a>D.2 將明確磁碟轉換成記憶體最佳化  
  
記憶體最佳化資料表變數不在 tempdb 中。 記憶體最佳化會導致速度加快，通常會加快 10 倍以上。  
  
只需要一個步驟，就能轉換成記憶體最佳化。 如下增強明確的 TYPE 建立，其新增：  
  
- 一個索引。 同樣地，每個記憶體最佳化資料表至少必須有一個索引。  
- MEMORY_OPTIMIZED = ON。  
  
  
  
```sql
CREATE TYPE dbo.typeTableD  
    AS TABLE  
    (  
        Column1  INT   NOT NULL   INDEX ix1,  
        Column2  CHAR(10)  
    )  
    WITH  
        (MEMORY_OPTIMIZED = ON);  
```  
  
  
  
大功告成。  
  
  
## <a name="e-prerequisite-filegroup-for-sql-server"></a>E. SQL Server 的必要條件 FILEGROUP  
  
在 Microsoft SQL Server 上，若要使用記憶體最佳化功能，您的資料庫必須有以 **MEMORY_OPTIMIZED_DATA**宣告的 FILEGROUP。  
  
- Azure SQL Database 不需要建立此 FILEGROUP。  
  
  
必要條件：  FILEGROUP 的下列 Transact-SQL 程式碼是本文稍後章節中很長之 T-SQL 程式碼範例的必要條件。  
  
1. 您必須使用 SSMS.exe 或可提交 T-SQL 的其他工具。  
2. 將範例 FILEGROUP T-SQL 程式碼貼到 SSMS 中。  
3. 編輯 T-SQL，將其特定名稱和目錄路徑變更為您慣用的名稱和目錄路徑。  
  - 除了最後一個目錄不能預先存在之外，FILENAME 值中的所有目錄都必須預先存在。  
4. 執行您所編輯的 T-SQL。  
  - 您不需要重複執行 FILEGROUP T-SQL，即使您在下一個小節中重複調整並重新執行速度比較 T-SQL 亦然。  
  
  
  
 
```sql
ALTER DATABASE InMemTest2  
    ADD FILEGROUP FgMemOptim3  
        CONTAINS MEMORY_OPTIMIZED_DATA;  
go  
ALTER DATABASE InMemTest2  
    ADD FILE  
    (  
        NAME = N'FileMemOptim3a',  
        FILENAME = N'C:\DATA\FileMemOptim3a'  
                    --  C:\DATA\    preexisted.  
    )  
    TO FILEGROUP FgMemOptim3;  
go  
```  


下列指令碼會為您建立檔案群組，並進行建議之資料庫的設定︰ [enable-in-memory-oltp.sql](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/in-memory-database/in-memory-oltp/t-sql-scripts/enable-in-memory-oltp.sql)
  
如需 FILE 和 FILEGROUP 之 `ALTER DATABASE ... ADD` 的詳細資訊，請參閱：  
  
- [ALTER DATABASE 檔案及檔案群組選項 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
- [記憶體最佳化檔案群組](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)    
  
  
## <a name="f-quick-test-to-prove-speed-improvement"></a>F. 快速測試以證明速度提升  
  
  
本節提供 Transact-SQL 程式碼，您可以執行以測試並比較使用記憶體最佳化資料表變數進行 INSERT-DELETE 所提升的速度。 此程式碼是由兩個幾乎相同的部分所組成，不同之處在於前半部分的資料表類型為記憶體最佳化。  
  
比較測試會持續約 7 秒。 若要執行範例：  
  
1. 必要條件：  您必須已執行上一節中的 FILEGROUP T-SQL。  
2. 執行下列 T-SQL INSERT-DELETE 指令碼。  
  - 請注意，'GO 5001' 陳述式會重新提交 T-SQL 5001 次。 您可以調整次數，然後重新執行。  
  
在 Azure SQL Database 中執行指令碼時，請務必從相同區域的 VM 執行。

  
```sql
PRINT ' ';  
PRINT '---- Next, memory-optimized, faster. ----';  

DROP TYPE IF EXISTS dbo.typeTableC_mem;  
go  
CREATE TYPE dbo.typeTableC_mem  -- !!  Memory-optimized.  
        AS TABLE  
        (  
            Column1  INT NOT NULL INDEX ix1,  
            Column2  CHAR(10)  
        )  
        WITH  
            (MEMORY_OPTIMIZED = ON);  
go  
DECLARE @dateString_Begin nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_Begin, '  = Begin time, _mem.');  
go  
SET NoCount ON;  
DECLARE @tvTableC dbo.typeTableC_mem;  -- !!  

INSERT INTO @tvTableC (Column1) values (1), (2);  
INSERT INTO @tvTableC (Column1) values (3), (4);  
DELETE @tvTableC;  

GO 5001  

DECLARE @dateString_End nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_End, '  = End time, _mem.');  
go  
DROP TYPE IF EXISTS dbo.typeTableC_mem;  
go  

---- End memory-optimized.  
-------------------------------------------------  
---- Start traditional on-disk.  

PRINT ' ';  
PRINT '---- Next, tempdb based, slower. ----';  

DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
go  
CREATE TYPE dbo.typeTableC_tempdb  -- !!  Traditional tempdb.  
    AS TABLE  
    (  
        Column1  INT NOT NULL ,  
        Column2  CHAR(10)  
    );  
go  
DECLARE @dateString_Begin nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_Begin, '  = Begin time, _tempdb.');  
go  
SET NoCount ON;  
DECLARE @tvTableC dbo.typeTableC_tempdb;  -- !!  

INSERT INTO @tvTableC (Column1) values (1), (2);  
INSERT INTO @tvTableC (Column1) values (3), (4);  
DELETE @tvTableC;  

GO 5001  

DECLARE @dateString_End nvarchar(64) =  
    Convert(nvarchar(64), GetUtcDate(), 121);  
PRINT Concat(@dateString_End, '  = End time, _tempdb.');  
go  
DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
go  
----  

PRINT '---- Tests done. ----';  

go  

/*** Actual output, SQL Server 2016:  

---- Next, memory-optimized, faster. ----  
2016-04-20 00:26:58.033  = Begin time, _mem.  
Beginning execution loop  
Batch execution completed 5001 times.  
2016-04-20 00:26:58.733  = End time, _mem.  

---- Next, tempdb based, slower. ----  
2016-04-20 00:26:58.750  = Begin time, _tempdb.  
Beginning execution loop  
Batch execution completed 5001 times.  
2016-04-20 00:27:05.440  = End time, _tempdb.  
---- Tests done. ----  
***/
```
  
  
  
## <a name="g-predict-active-memory-consumption"></a>G. 預測使用中記憶體耗用量  
  
您可以透過下列資源，了解如何預測記憶體最佳化資料表的使用中記憶體需求：  
  
- [估計記憶體最佳化資料表的記憶體需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [經記憶體最佳化資料表中的資料表和資料列大小：範例計算](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
針對較大的資料表變數，非叢集索引會使用比記憶體最佳化「資料表」  更多的記憶體。 資料列計數和索引鍵愈大，所增加的差異愈多。  
  
如果每次存取只能使用一個索引鍵值來存取記憶體資料表變數，則雜湊索引可能比非叢集索引更適合。 不過，如果您無法估計正確的 BUCKET_COUNT，則非叢集索引是不錯的次要選擇。  
  
## <a name="h-see-also"></a>H. 另請參閱  
  
- [經記憶體最佳化的資料表](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)。

- [為記憶體最佳化的物件定義持久性](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)。

- [降低發生不當記憶體不足錯誤可能性的累積更新，已於 2017 年 9 月部落格中宣告](https://support.microsoft.com/help/4025208/fix-memory-leak-occurs-when-you-use-memory-optimized-tables-in-microso)
    - [SQL Server 2016 組建版本](https://support.microsoft.com/help/3177312/sql-server-2016-build-versions)提供版本、Service Pack 和累積更新的完整詳細資料。
    - 這些偶發的不當錯誤不會出現在 SQL Server Enterprise Edition 中。

