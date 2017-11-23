---
title: "DBCC FREEPROCCACHE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FREEPROCCACHE_TSQL
- FREEPROCCACHE
- DBCC_FREEPROCCACHE_TSQL
- DBCC FREEPROCCACHE
dev_langs: TSQL
helpviewer_keywords:
- freeing procedure cache
- removing procedure cache elements
- deleting procedure cache elements
- DBCC FREEPROCCACHE statement
- procedure cache [SQL Server]
- clearing procedure cache
ms.assetid: 0e09d210-6f23-4129-aedb-3d56b2980683
caps.latest.revision: "61"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ae416ab23f27a7f71951ac05a6c69d0abb00a90d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-freeproccache-transact-sql"></a>DBCC FREEPROCCACHE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

從計畫快取移除所有元素；指定計畫控制代碼或 SQL 控制代碼，從計畫快取移除特定的計畫；或是移除與指定的資源集區相關聯的所有快取項目。

>[!NOTE]
>DBCC FREEPROCCACHE 不會清除原生編譯預存程序的執行統計資料。 程序快取沒有包含原生編譯預存程序的相關資訊。 從程序執行收集而來的執行統計資料會出現在執行統計資料 Dmv: [sys.dm_exec_procedure_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)和[sys.dm_exec_query_plan &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
SQL Server 的語法：

```sql
DBCC FREEPROCCACHE [ ( { plan_handle | sql_handle | pool_name } ) ] [ WITH NO_INFOMSGS ]  
```  

Azure SQL 資料倉儲和 Parallel Data Warehouse 的語法：
  
```sql
DBCC FREEPROCCACHE [ ( COMPUTE | ALL ) ] 
     [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>引數  
 ({ *plan_handle* | *sql_handle* | *pool_name* })  
*plan_handle*唯一識別批次已經執行且其計畫位於計畫快取的查詢計劃。 *plan_handle*是**varbinary(64)** ，且可以從下列動態管理物件取得：  
 -   [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  

*sql_handle*来清除之批次的 SQL 控制代碼。 *sql_handle*是**varbinary(64)** ，且可以從下列動態管理物件取得：  
 -   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
 -   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
 -   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
 -   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
 -   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  

*pool_name*是資源管理員資源集區的名稱。 *pool_name*是**sysname**而且可以藉由查詢取得[sys.dm_resource_governor_resource_pools](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)動態管理檢視。  
 若要將資源管理員工作負載群組與資源集區產生關聯，查詢[sys.dm_resource_governor_workload_groups](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)動態管理檢視。 工作階段的工作負載群組的相關資訊，如查詢[sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)動態管理檢視。  

  
 WITH NO_INFOMSGS  
 隱藏所有參考訊息。  
  
 COMPUTE  
 清除查詢計劃快取中的每個計算節點。 這是預設值。  
  
 ALL  
 從每個計算節點和 [控制] 節點，請清除查詢計劃快取。  

> [!NOTE]
> 從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]、`ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE`清除程序 （計劃） 快取範圍中的資料庫。

## <a name="remarks"></a>備註  
請利用 DBCC FREEPROCCACHE 小心清除計畫快取。 清除程序 （計劃） 快取會使所有的計劃被收回或傳入的查詢執行會編譯新的計畫，而不要重複使用任何先前的快取的計畫。 

這可能會造成的新編譯增加而增加數字的查詢效能突然暫時下降。 針對每次清除計畫快取的快取存放區，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔會包含下列參考訊息：「由於 'DBCC FREEPROCCACHE' 或 'DBCC FREESYSTEMCACHE' 作業，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 '%s' 快取存放區 (計畫快取的一部分) 發生 %d 次快取存放區排清。」 只要在該時間間隔內快取發生排清，這個訊息就會每五分鐘記錄一次。

下列重新設定作業也會清除程序快取：
-   存取檢查快取 Bucket 計數  
-   存取檢查快取配額  
-   clr enabled  
-   平行處理原則的成本臨界值  
-   cross db ownership chaining  
-   索引建立記憶體  
-   平行處理原則的最大程度  
-   max server memory  
-   max text repl size  
-   最大工作者執行緒  
-   min memory per query  
-   min server memory  
-   查詢管理者成本限制  
-   查詢等候  
-   remote query timeout  
-   user options  
  
## <a name="result-sets"></a>結果集  
當未指定 WITH NO_INFOMSGS 子句時，DBCC FREEPROCCACHE 會傳回:"DBCC 執行已完成。 如果 DBCC 印出錯誤訊息，請連絡您的系統管理員」。
  
## <a name="permissions"></a>Permissions  
適用於： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 
- 需要伺服器的 ALTER SERVER STATE 權限。  

適用於：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
- 需要 DB_OWNER 固定的伺服器角色的成員資格。  

## <a name="general-remarks-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>一般備註[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
可以同時執行多個 DBCC FREEPROCCACHE 命令。
在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]清除計畫快取可能會導致查詢效能降低暫存傳入的查詢編譯新的計畫，而不要重複使用任何先前的快取計畫。 

DBCC FREEPROCCACHE （運算） 只會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]計算節點上執行時重新編譯查詢。 不會造成[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]平行查詢計畫所產生的控制節點上，重新編譯。
DBCC FREEPROCCACHE 可以在執行期間取消。
  
## <a name="limitations-and-restrictions-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>限制的事項[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
DBCC FREEPROCCACHE 不可以在交易內執行。
不支援 DBCC FREEPROCCAHCE 解釋陳述式中。
  
## <a name="metadata-for-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>中繼資料[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
新的資料列加入 sys.pdw_exec_requests 系統檢視表，當執行 DBCC FREEPROCCACHE。

## <a name="examples-includessnoversionincludesssnoversion-mdmd"></a>範例：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
### <a name="a-clearing-a-query-plan-from-the-plan-cache"></a>A. 從計畫快取清除查詢計劃  
下列範例會從計畫快取中指定查詢計劃控制代碼，藉以清除查詢計劃。 為確保範例查詢位於計畫快取中，會先執行查詢。 `sys.dm_exec_cached_plans`和`sys.dm_exec_sql_text`動態管理檢視會查詢來傳回查詢的計畫控制代碼。 

然後會將結果集中的計畫控制代碼值插入到 `DBCC FREEPROCACHE` 陳述式中，就可以從計畫快取中僅移除該計畫。
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT * FROM Person.Address;  
GO  
SELECT plan_handle, st.text  
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st  
WHERE text LIKE N'SELECT * FROM Person.Address%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
plan_handle                                         text  
--------------------------------------------------  -----------------------------  
0x060006001ECA270EC0215D05000000000000000000000000  SELECT * FROM Person.Address;  
  
(1 row(s) affected)
 ```
 
```sql  
-- Remove the specific plan from the cache.  
DBCC FREEPROCCACHE (0x060006001ECA270EC0215D05000000000000000000000000);  
GO  
```  
  
### <a name="b-clearing-all-plans-from-the-plan-cache"></a>B. 從計畫快取清除所有計畫  
下列範例會從計畫快取中清除所有元素。 WITH`NO_INFOMSGS`指定子句可防止資訊訊息顯示。
  
```sql  
DBCC FREEPROCCACHE WITH NO_INFOMSGS;  
```  
  
### <a name="c-clearing-all-cache-entries-associated-with-a-resource-pool"></a>C. 清除與資源集區相關聯的所有快取項目  
下列範例會清除與指定之資源集區有關聯的所有快取項目。 `sys.dm_resource_governor_resource_pools`檢視第一次查詢來取得的值*pool_name*。
  
```sql  
SELECT * FROM sys.dm_resource_governor_resource_pools;  
GO  
DBCC FREEPROCCACHE ('default');  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-dbcc-freeproccache-basic-syntax-examples"></a>D. DBCC FREEPROCCACHE 基本語法範例  
下列範例會移除所有現有的查詢計畫快取來自計算節點。 雖然內容設定為 UserDbSales，所有資料庫的計算節點查詢計劃快取將會移除。 WITH NO_INFOMSGS 子句可防止結果中出現資訊訊息。  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE) WITH NO_INFOMSGS;
```  
  
 下列範例具有相同的結果與前一個範例中，不同之處在於告知性訊息會顯示在結果中。  
  
```sql
USE UserDbSales;  
DBCC FREEPROCCACHE (COMPUTE);  
```  
  
當要求參考用訊息，且執行成功時，查詢結果會有每個計算節點的一行。
  
### <a name="e-granting-permission-to-run-dbcc-freeproccache"></a>E. 授與權限來執行 DBCC FREEPROCCACHE  
下列範例會提供登入執行 DBCC FREEPROCCACHE David 權限。  
  
```sql
GRANT ALTER SERVER STATE TO David; 
GO
```  
  
## <a name="see-also"></a>請參閱＜  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[資源管理員](../../relational-databases/resource-governor/resource-governor.md)  
[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
  
  
