---
title: sys.dm_exec_query_plan_stats (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: 92e5aaf103c1c8d08b8527bf859415686fd5f4f8
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993623"
---
# <a name="sysdmexecqueryplanstats-transact-sql"></a>sys.dm_exec_query_plan_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-asdb-xxxx-xxx.md)]

會傳回相當於先前快取的查詢計劃的最後一個已知的實際執行計畫。

## <a name="syntax"></a>語法

```
sys.dm_exec_query_plan_stats(plan_handle)  
``` 

## <a name="arguments"></a>引數 
*plan_handle*  
可唯一識別查詢執行計畫，該批次已經執行的語彙基元且其計畫位於計畫快取，或正在執行。 *plan_handle*已**varbinary(64)**。   

*Plan_handle*可以從下列動態管理物件取得：  
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  

## <a name="table-returned"></a>傳回的資料表

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|
|**dbid**|**smallint**|當編譯對應於這個計畫的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，作用中內容資料庫的識別碼。 對於隨選和準備的 SQL 陳述式而言，則為編譯陳述式的資料庫識別碼。<br /><br /> 資料行可為 Null。|  
|**objectid**|**int**|這個查詢計畫的物件識別碼 (如預存程序或使用者自訂函數)。 針對隨選和備妥的批次，這個資料行是**null**。<br /><br /> 資料行可為 Null。|  
|**number**|**smallint**|編號預存程序整數。 例如，群組的程序**訂單**可能名為應用程式**orderproc; 1**， **orderproc; 2**，依此類推。 針對隨選和備妥的批次，這個資料行是**null**。<br /><br /> 資料行可為 Null。|  
|**encrypted**|**bit**|指出對應的預存程序是否加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 加密<br /><br /> 資料行不可為 Null。|  
|**query_plan**|**xml**|包含上次已知的執行階段使用指定的實際查詢執行計畫顯示計畫表示法*plan_handle*。 顯示計畫是 XML 格式。 每個包含諸如特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、預存程序呼叫和使用者自訂函數呼叫的批次，都會產生一份計畫。<br /><br /> 資料行可為 Null。| 

## <a name="remarks"></a>備註
這個系統函數可從[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]CTP 2.4。

這是選擇加入的功能，需要啟用[追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 2451。 開頭[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]CTP 2.5 然後在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，以在資料庫層級完成這項作業，請參閱中的 LAST_QUERY_PLAN_STATS 選項[ALTER DATABASE SCOPED CONFIGURATION &#40;-&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。

這個系統函數運作**輕量級**查詢分析基礎結構的執行統計資料。 如需詳細資訊，請參閱[查詢分析基礎結構](../../relational-databases/performance/query-profiling-infrastructure.md)。  

在下列情況中，執行程序表輸出**相當於實際執行計畫**會傳回**query_plan**傳回之資料表的資料行**sys.dm_exec_query_plan_統計資料**:  

-   此計劃可在[sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)。     
    **AND**    
-   複雜或耗用資源所執行的查詢。

在下列情況中，**簡化<sup>1</sup>** 程序表輸出中會傳回**query_plan**傳回之資料表的資料行**sys.dm_exec_query_plan_stats**:  

-   此計劃可在[sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)。     
    **AND**    
-   查詢相當簡單，通常分類為 OLTP 工作負載的一部分。

<sup>1</sup>開頭[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]CTP 2.5，這是指 Showplan 只包含根節點運算子 （選取）。 針對[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]這是指做為可透過快取計畫的 CTP 2.4 `sys.dm_exec_cached_plans`。

在下列情況中，**會傳回任何輸出**從**sys.dm_exec_query_plan_stats**:

-   使用指定的查詢計劃*plan_handle*已從計畫快取中收回。     
    **OR**    
-   查詢計劃則沒有可快取在第一時間。 如需詳細資訊，請參閱 <<c0> [ 執行計畫快取和重複使用](../../relational-databases/query-processing-architecture-guide.md#execution-plan-caching-and-reuse)。
  
> [!NOTE] 
> 基於中允許的巢狀層級數目的限制**xml**資料類型**sys.dm_exec_query_plan**無法傳回達到或超過 128 個層級的巢狀項目查詢計劃。 在舊版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這種情況的查詢計畫無法傳回並產生[錯誤 6335](../../relational-databases/errors-events/database-engine-events-and-errors.md#errors-6000-to-6999)。 在  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 和更新版本中， **query_plan**資料行會傳回 NULL。  

## <a name="permissions"></a>Permissions  
 需要伺服器的 `VIEW SERVER STATE` 權限。  

## <a name="examples"></a>範例  
  
### <a name="a-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan"></a>A. 尋找特定的快取計劃的最後已知的實際查詢執行計畫  
 下列範例會查詢**sys.dm_exec_cached_plans**來尋找有趣的計劃並複製其`plan_handle`從輸出中。  
  
```sql  
SELECT * FROM sys.dm_exec_cached_plans;  
GO  
```  
  
然後，若要取得的最後一個已知的實際查詢執行計畫，使用 複製`plan_handle`搭配系統函數**sys.dm_exec_query_plan_stats**。  
  
```sql  
SELECT * FROM sys.dm_exec_query_plan_stats(< copied plan_handle >);  
GO  
```   

### <a name="b-looking-at-last-known-actual-query-execution-plan-for-all-cached-plans"></a>B. 尋找所有快取計畫的最後已知的實際查詢執行計畫
  
```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps;  
GO  
```   

### <a name="c-looking-at-last-known-actual-query-execution-plan-for-a-specific-cached-plan-and-query-text"></a>C. 尋找特定的快取計劃和查詢文字的已知的實際查詢執行計劃在上一次

```sql  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp
CROSS APPLY sys.dm_exec_sql_text(plan_handle) AS st
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle) AS qps
WHERE st.text LIKE 'SELECT * FROM Person.Person%';  
GO  
```   

### <a name="d-look-at-cached-events-for-trigger"></a>D. 查看觸發程序快取事件

```sql
SELECT *
FROM sys.dm_exec_cached_plans
CROSS APPLY sys.dm_exec_query_plan_stats(plan_handle)
WHERE objtype ='Trigger';
GO
```

## <a name="see-also"></a>另請參閱
  [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  

