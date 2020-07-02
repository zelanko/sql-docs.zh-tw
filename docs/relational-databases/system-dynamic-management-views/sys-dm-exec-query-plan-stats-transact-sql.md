---
title: sys.databases dm_exec_query_plan_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_plan_stats
- sys.dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats_TSQL
- dm_exec_query_plan_stats
helpviewer_keywords:
- sys.dm_exec_query_plan_stats management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfacb
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 3bd7aa786466f3bde9aa42d75437d2406ef1e808
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734746"
---
# <a name="sysdm_exec_query_plan_stats-transact-sql"></a>sys.databases dm_exec_query_plan_stats （Transact-sql）
[!INCLUDE[SQL Server 2019](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

傳回先前快取之查詢計劃的最後已知實際執行計畫的對等。

## <a name="syntax"></a>語法

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>引數 
*plan_handle*  
這是一個標記，可唯一識別已執行之批次的查詢執行計畫，且其計畫位於計畫快取中，或目前正在執行。 *plan_handle*為**Varbinary （64）**。   

*Plan_handle*可以從下列動態管理物件取得：  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [dm_exec_procedure_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [dm_exec_trigger_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>傳回的資料表

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|當編譯對應於這個計畫的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，作用中內容資料庫的識別碼。 對於隨選和準備的 SQL 陳述式而言，則為編譯陳述式的資料庫識別碼。<br /><br /> 資料行可為 Null。|  
|**objectid**|**int**|這個查詢計畫的物件識別碼 (如預存程序或使用者自訂函數)。 若為特定和準備批次，這個資料行是 **Null**。<br /><br /> 資料行可為 Null。|  
|**number**|**smallint**|編號預存程序整數。 例如，**orders** 應用程式的一組程序可以命名為 **orderproc;1**、**orderproc;2**，依此類推。 若為特定和準備批次，這個資料行是 **Null**。<br /><br /> 資料行可為 Null。|  
|**加密**|**bit**|指出對應的預存程序是否加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 加密<br /><br /> 資料行不可為 Null。|  
|**query_plan**|**xml**|包含以*plan_handle*指定之實際查詢執行計畫的上次已知執行時間顯示計畫標記法。 顯示計畫是 XML 格式。 每個包含諸如特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、預存程序呼叫和使用者自訂函數呼叫的批次，都會產生一份計畫。<br /><br /> 資料行可為 Null。| 

## <a name="remarks"></a>備註
從 CTP 2.4 開始提供此系統函數 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 。

這是選擇加入的功能，需要啟用[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451。 從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5 開始，若要在資料庫層級完成此作業，請參閱[ ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) 中的 LAST_QUERY_PLAN_STATS 選項。

此系統函數可在**輕量**查詢執行統計資料分析基礎結構底下運作。 如需詳細資訊，請參閱[查詢分析基礎結構](../../relational-databases/performance/query-profiling-infrastructure.md)。  

Sys 的執行程式表輸出 dm_exec_query_plan_stats 包含下列資訊：
-  在快取計畫中找到的所有編譯時間資訊
-  執行時間資訊，例如每個運算子的實際資料列數目、查詢 CPU 時間與執行時間總計、溢出警告、實際 DOP、使用的記憶體上限和授與的記憶體

在下列情況下，會在**dm_exec_query_plan_stats**的傳回資料表的**query_plan**資料行中，傳回**相當於實際執行計畫**的顯示計畫輸出：  

-   您可以在 sys.databases 中找到此方案[dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)。     
    **和**    
-   正在執行的查詢很複雜或耗用資源。

在下列情況下，會在傳回之資料表的**query_plan**資料行中，傳回一個**簡化的<sup>1</sup> **執行程式表輸出，以供**dm_exec_query_plan_stats**：  

-   您可以在 sys.databases 中找到此方案[dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)。     
    **和**    
-   查詢夠簡單，通常會分類為 OLTP 工作負載的一部分。

<sup>1</sup>從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.5 開始，這是指只包含根節點運算子（SELECT）的執行程式表。 對於 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] CTP 2.4，這是指透過提供的快取計畫 `sys.dm_exec_cached_plans` 。

在下列情況下，從**sys. dm_exec_query_plan_stats****不會傳回任何輸出**：

-   使用*plan_handle*所指定的查詢計劃已從計畫快取中收回。     
    **OR**    
-   查詢計劃無法在第一個位置快取。 如需詳細資訊，請參閱[執行計畫快取和重複使用](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)。
  
> [!NOTE] 
> 由於**xml**資料類型所允許的嵌套層級數目有限制，因此**dm_exec_query_plan**無法傳回符合或超過128個嵌套元素層級的查詢計劃。 在舊版的中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這種情況會使查詢計劃無法傳回，並產生[錯誤 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999)。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 和更新版本中， **query_plan**資料行傳回 Null。  

## <a name="permissions"></a>權限  
 需要伺服器的 `VIEW SERVER STATE` 權限。  

## <a name="examples"></a>範例  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. 查看特定快取計畫的最後已知實際查詢執行計畫  
 下列範例會查詢**dm_exec_cached_plans sys.databases** ，以尋找有趣的計畫，並 `plan_handle` 從輸出複製其。  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
然後，若要取得最後一個已知的實際查詢執行計畫，請使用 `plan_handle` 以系統函數**sys.databases dm_exec_query_plan_stats**複製的。  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. 正在查看所有快取計畫的最後已知實際查詢執行計畫
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. 查看特定快取計畫和查詢文字的最後已知實際查詢執行計畫

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. 查看觸發程式的快取事件

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>另請參閱
  [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [&#40;Transact-sql&#41;執行相關的動態管理檢視](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

