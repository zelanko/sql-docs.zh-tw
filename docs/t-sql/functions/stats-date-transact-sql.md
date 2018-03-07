---
title: "STATS_DATE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATS_DATE_TSQL
- STATS_DATE
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], last time updated
- STATS_DATE function
- query optimization statistics [SQL Server], last time updated
- last time statistics updated
- stats update date
ms.assetid: f9ec3101-1e41-489d-b519-496a0d6089fb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de308046d069b6efa6115cf1efae33af7c07128c
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="statsdate-transact-sql"></a>STATS_DATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對資料表或索引檢視表的統計資料傳回最近更新的日期。  
  
 如需有關更新統計資料的詳細資訊，請參閱[統計資料](../../relational-databases/statistics/statistics.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STATS_DATE ( object_id , stats_id )  
```  
  
## <a name="arguments"></a>引數  
 *object_id*  
 包含統計資料之資料表或索引檢視表的識別碼。  
  
 *stats_id*  
 統計資料物件的識別碼。  
  
## <a name="return-types"></a>傳回類型  
 傳回**datetime**成功。 傳回**NULL**若未建立的統計資料的 blob。  
  
## <a name="remarks"></a>備註  
 系統函數可用在選取清單中，在 WHERE 子句中，而且可以使用運算式的地方。  
 
 統計資料更新將日期儲存在[統計資料的 blob 物件](../../relational-databases/statistics/statistics.md#DefinitionQOStatistics)搭配[長條圖](../../relational-databases/statistics/statistics.md#histogram)和[密度向量](../../relational-databases/statistics/statistics.md#density)、 中繼資料中找不到。 讀取任何資料時產生統計資料，不建立的統計資料的 blob，並在日期不是可用。 這是篩選的統計資料述詞未傳回任何資料列，或新的空白資料表的情況。
 
 如果統計資料對應到索引， *stats_id*值[sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)目錄檢視等同於*index_id*值[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視。
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 固定資料庫角色中的成員資格或權限，才能檢視資料表或索引檢視表的中繼資料。  
  
## <a name="examples"></a>範例  
  
### <a name="a-return-the-dates-of-the-most-recent-statistics-for-a-table"></a>A. 針對資料表傳回最近更新統計資料的日期  
 下列範例會針對 `Person.Address` 資料表的每個統計資料物件傳回最近更新的日期。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_update_date  
FROM sys.stats   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
 如果統計資料對應到索引， *stats_id*值[sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)目錄檢視等同於*index_id*值[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視，而且下列查詢會傳回與之前查詢相同的結果。 如果統計資料未對應到索引，統計資料會在 sys.stats 結果中而不是 sys.indexes 結果中。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-learn-when-a-named-statistics-was-last-updated"></a>B. 了解具名的統計資料上次更新  
 下列範例會建立 DimCustomer 資料表的 [姓氏] 資料行的統計資料。 然後，它會執行查詢，以顯示統計資料的日期。 然後它更新統計資料，並執行查詢，一次以顯示更新的日期。  
  
```sql
--First, create a statistics object  
USE AdventureWorksPDW2012;  
GO  
CREATE STATISTICS Customer_LastName_Stats  
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName)  
WITH SAMPLE 50 PERCENT;  
GO  
  
--Return the date when Customer_LastName_Stats was last updated  
USE AdventureWorksPDW2012;  
GO  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO  
  
--Update Customer_LastName_Stats so it will have a different timestamp in the next query  
GO  
UPDATE STATISTICS dbo.dimCustomer (Customer_LastName_Stats);  
  
--Return the date when Customer_LastName_Stats was last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO    
```  
  
### <a name="c-view-the-date-of-the-last-update-for-all-statistics-on-a-table"></a>C. 檢視的資料表上的所有統計資料上次更新日期  
 這個範例會傳回 DimCustomer 資料表上的每個統計資料物件上次更新的日期。  
  
```sql  
--Return the dates all statistics on the table were last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
 如果統計資料對應到索引， *stats_id*值[sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)目錄檢視等同於*index_id*值[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)目錄檢視，而且下列查詢會傳回與之前查詢相同的結果。 如果統計資料未對應到索引，統計資料會在 sys.stats 結果中而不是 sys.indexes 結果中。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_autostats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [統計資料](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
  
  

