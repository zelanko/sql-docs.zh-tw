---
title: "時態表 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/11/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e442303d-4de1-494e-94e4-4f66c29b5fb9
caps.latest.revision: 47
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 47
---
# 時態表
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 以資料庫功能的形式引進了對系統建立版本時態表的支援，其帶入內建支援，提供儲存在資料表中任何時間點資料的相關資訊，而不是只有在目前時間為正確的資料。 Temporal 是 ANSI SQL 2011 中引進的資料庫功能， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]現在可加以支援。  
  
 **快速入門**  
  
-   **開始使用：**  
  
    -   [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)  
  
    -   [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)  
  
    -   [時態表使用案例](../../relational-databases/tables/temporal-table-usage-scenarios.md)  
  
    -   [開始使用 Azure SQL 資料庫的時態表](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/)  
  
-   **範例:**  
  
    -   [建立系統建立版本的時態表](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)  
  
    -   [使用記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)  
  
    -   [修改系統建立版本時態表中的資料](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)  
  
    -   [查詢系統建立版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)  
  
    -   **下載 Adventure Works 範例資料庫︰** 若要開始使用時態表，請下載 [適用於 SQL Server 2016 CTP3 的 AdventureWorks 資料庫](https://www.microsoft.com/download/details.aspx?id=49502) 與指令碼範例，然後遵循 'Temporal' 資料夾中的指示  
  
-   **語法：**  
  
    -   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
    -   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
    -   [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
-   **視訊︰** 如需為時 20 分鐘的 Temporal 討論，請參閱 [SQL Server 2016 的 Temporal](http://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)。  
  
## 什麼是系統建立版本的時態表？  
 系統建立版本的時態表是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中全新類型的使用者資料表，其設計目的是為了保留資料變更的完整歷程記錄，並允許簡易的時間點分析。 由於每個資料列的有效期間是由系統 (也就是資料庫引擎) 所管理，因此這種類型的時態表稱為系統設定版本的時態表。  
  
 每個時態表皆有兩個明確定義的資料行，分別各具 **datetime2** 資料類型。 這些資料行稱為期間資料行。 這些期間資料行由系統專用，用來在每次修改資料列時記錄每個資料列的有效期間。  
  
 除了這些期間資料行以外，時態表也包含使用鏡像結構描述的另一個資料表參考。 系統會使用此資料表，在每次時態表中的資料列進行更新或刪除時，自動儲存資料列的先前版本。 此額外資料表稱為歷程記錄資料表，而儲存目前 (實際) 資料列版本的主資料表稱為目前資料表，或簡稱為時態表。 建立時態表時，使用者可以指定現有的歷程記錄資料表 (必須與結構描述相容)，或讓系統建立預設歷程記錄資料表。  
  
## 為何選擇時態表？  
 實際資料來源為動態，且商務決策通常依賴分析師可從資料演進獲得的見解。 時態表的使用案例包括︰  
  
-   稽核所有資料變更並視需求執行資料鑑識  
  
-   重新建構過去任何時間的資料狀態  
  
-   計算一段時間的趨勢  
  
-   維護決策支援應用程式的緩時變更維度  
  
-   從資料意外變更與應用程式錯誤中復原  
  
## 時態表如何運作？  
 資料表的系統建立版本會實作為一對資料表、目前的資料表和歷程記錄資料表。 在這些資料表中，下列兩個額外的 **datetime2** 資料行用來定義每個資料列的有效期間︰  
  
-   期間開始資料行︰系統會記錄此資料行中資料列的開始時間，通常表示為 **SysStartTime** 資料行。  
  
-   期間結束資料行︰系統會記錄此資料行中資料列的結束時間，通常表示於 **SysEndTime** 資料行。  
  
 目前資料表包含每個資料列的目前值。 歷程記錄資料表包含每個資料列各個先前的值 (如果有的話)，以及週期的有效開始時間和結束時間。  
  
 ![Temporal-HowWorks](../../relational-databases/tables/media/temporal-howworks.PNG "Temporal-HowWorks")  
  
 下列簡易範例說明在假設性的 HR 資料庫中「員工」資訊的案例：  
  
```  
CREATE TABLE dbo.Employee   
(    
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED   
  , [Name] nvarchar(100) NOT NULL  
  , [Position] varchar(100) NOT NULL   
  , [Department] varchar(100) NOT NULL  
  , [Address] nvarchar(1024) NOT NULL  
  , [AnnualSalary] decimal (10,2) NOT NULL  
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START  
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END  
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
 )    
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));  
```  
  
 **INSERTS：**在 **INSERT** 上，系統會根據系統時鐘將 **SysStartTime** 資料行的值設定為目前交易的開始時間 (以 UTC 時區為準)，並將 **SysEndTime** 資料行的值指派至 9999-12-31 的最大值。 這會將資料列標示為開啟。  
  
 **UPDATES：**在 **UPDATE** 上，系統會將資料列的先前值儲存在歷程記錄資料表中，並根據系統時鐘將 **SysEndTime** 資料行的值設定為目前交易的開始時間 (以 UTC 時區為準)。 這會將資料列標示為關閉，並記錄資料列有效的期間。 在目前資料表中，系統會以資料列的新值更新記錄，並根據系統時鐘將 **SysStartTime** 資料行的值設定為目前交易的開始時間 (以 UTC 時區為準)。 **SysEndTime** 資料行目前資料表中更新資料列的值保持為 9999-12-31 的最大值。  
  
 **DELETES：**在 **DELETE** 上，系統會將資料列的先前值儲存在歷程記錄資料表中，並根據系統時鐘將 **SysEndTime** 資料行的值設定為目前交易的開始時間 (以 UTC 時區為準)。 這會將資料列標示為關閉，並記錄先前資料列有效的期間。 在目前資料表中，資料列受到移除。 目前資料表的查詢不會傳回此資料列。 只有處理歷程記錄資料的查詢會傳回資料列已關閉的資料。  
  
 **MERGE︰**在 **MERGE** 上，作業行為完全就像執行最多三個陳述式 ( **INSERT**、**UPDATE** 和/或 **DELETE**) 一樣，視 **MERGE** 陳述式中指定為動作的內容而定。  
  
> [!IMPORTANT]  
>  系統 datetime2 資料行中所記錄的時間是依據交易本身的開始時間。 例如，在單一交易中插入的所有資料列，在資料行中都會記錄相同的 UTC 時間，且對應到 **SYSTEM_TIME**。  
  
## 如何查詢時態表？  
 **SELECT** 陳述式 **FROM**\<資料表> 子句具有新子句 **FOR SYSTEM_TIME**附帶五個時態特定的子子句，以在目前和歷程記錄資料表之間查詢資料。 這個新 **SELECT** 陳述式語法直接受到單一資料表支援，透過多個聯結以及在多個時態表上檢視進行傳播。  
  
 ![Temporal-Querying](../../relational-databases/tables/media/temporal-querying.PNG "Temporal-Querying")  
  
 下列查詢會搜尋「員工」資料列的資料列版本，搜尋條件為 EmployeeID = 1000，且在 2014 年 1 月 1 日和 2015 年 1 月 1 日之間 (包括上限) 至少有在一段時間為作用中：  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME    
        BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'   
            WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
> [!NOTE]  
>  ** SYSTEM_TIME** 會篩選掉具有有效期間且持續時間為零的資料列 (**SysStartTime** = **SysEndTime**)。  
> 如果您在相同交易內的相同主索引鍵上執行多個更新，這些資料列就會產生。  
> 在此情況下，Temporal 會查詢介面唯一資料列交易之前的版本，以及交易之後變為實際的版本。  
> 如果您需要在分析中加入這些資料列，請直接查詢記錄資料表。  
  
 在下表中，合格資料列資料行中的 SysStartTime 代表所查詢資料表中 **SysStartTime** 資料行中的值，而 **SysEndTime** 代表所查詢資料表中 **SysEndTime** 資料行中的值。 如需完整的語法和範例，請參閱 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) 和[查詢系統建立版本時態表中的資料](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)。  
  
|運算式|查詢資料列|描述|  
|----------------|---------------------|-----------------|  
|**AS OF**\<日期時間>|SysStartTime \<= date_time AND SysEndTime > date_time|傳回含有資料列的資料表，資料列內含的值是過去指定時間點的實際 (目前) 值。 就內部而言，時態表和其歷程記錄資料表之間會執行等位，且會將結果篩選為傳回資料列中的值，該資料列在 \<日期時間> 參數所指定的時間點為有效。 資料列的值會被視為有效，如果 *system_start_time_column_name* 值小於或等於 \<日期時間> 參數值，且 *system_end_time_column_name* 值大於 \<日期時間> 參數值。|  
|**FROM**\<開始日期時間>**TO**\<結束日期時間>|SysStartTime \< end_date_time AND SysEndTime > start_date_time|傳回資料表，其中內含所有資料列版本的值，該值在所指定的時間範圍內有效，而不論其是否在 FROM 引數的 \<開始日期時間> 參數值之前為作用中，或是在 TO 引數的 \<結束日期時間> 參數值之後就不在作用中。 就內部而言，時態表和其歷程記錄資料表之間會執行等位，且會將結果篩選為傳回所有資料列版本的值，該值在指定的時間範圍任何時間點內皆為作用中。 包含恰好在 FROM 端點所定義的範圍下限變為作用中的資料列，而不包含恰好在 TO 端點所定義的範圍上限變為作用中的資料列。|  
|**BETWEEN**\<開始日期時間>**AND**\<結束日期時間>|SysStartTime \<= end_date_time AND SysEndTime > start_date_time|如同上方 **FOR SYSTEM_TIME FROM**\<開始日期時間>**TO**\<結束日期時間> 中的描述，唯一的差別在於所傳回資料列的資料表內含的資料列，在 \<結束日期時間> 端點所定義的範圍上限變為作用中。|  
|**CONTAINED IN** (\<開始日期時間> , \<結束日期時間>)|SysStartTime >= start_date_time AND SysEndTime \<= end_date_time|傳回資料表，其中內含所有資料列版本的值，該值在 CONTAINED IN 引數兩個日期時間值所定義的指定時間範圍內為開啟及關閉。 包含恰好在範圍下限變為作用中的資料列，或是恰好在範圍上限就不在作用中的資料列。|  
|**ALL**|所有資料列|傳回屬於目前和歷程記錄資料表的資料列聯集。|  
  
> [!NOTE]  
>  您可以選擇隱藏這些期間資料行，讓未明確參考這些期間資料行的查詢不會傳回這些資料行 (**SELECT \* FROM** \<資料表> 案例)。 若要傳回隱藏的資料行，只需明確地參考查詢中的隱藏資料行。 同樣地，**INSERT** 和 **BULK INSERT** 陳述式將繼續進行，就如同這些新期間資料行不存在一般 (且資料行值將會自動填入)。 如需使用 **HIDDEN** 子句的詳細資料，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 和 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)。  
  
## 這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Tables%20page)  
  
## 另請參閱  
 [開始使用系統建立版本的時態表](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [時態表使用案例](../../relational-databases/tables/temporal-table-usage-scenarios.md)   
 [時態表考量與限制](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [對時態表進行資料分割](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [時態表安全性](../../relational-databases/tables/temporal-table-security.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  