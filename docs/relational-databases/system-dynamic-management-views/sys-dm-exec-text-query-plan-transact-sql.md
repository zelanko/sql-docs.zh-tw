---
title: sys.databases dm_exec_text_query_plan （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d23813078c2a90b18af0a1df48079b571e77a13
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983136"
---
# <a name="sysdm_exec_text_query_plan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

針對 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次或批次內的特定陳述式，以文字格式傳回顯示計畫。 計畫控制碼指定的查詢計劃可以是快取或目前正在執行。 這個資料表值函式類似于[sys.databases dm_exec_query_plan &#40; &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)，但具有下列差異：  
  
-   查詢計畫的輸出會以文字格式傳回。  
-   查詢計畫的輸出沒有大小限制。  
-   可以指定批次內的個別陳述式。  
  
**適用于**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本）、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>引數  
*plan_handle*  
這是一個標記，可唯一識別已執行之批次的查詢執行計畫，且其計畫位於計畫快取中，或目前正在執行。 *plan_handle*為**Varbinary （64）** 。   

*Plan_handle*可以從下列動態管理物件取得： 
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys. dm_exec_procedure_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;-SQL&AMP;&#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
*statement_start_offset* |0 |預設  
表示資料列於其批次或保存物件的文字中描述之查詢的起始位置 (以位元組為單位)。 *statement_start_offset*為**int**。值為0表示批次的開頭。 預設值是 0。  
  
您可以從下列動態管理物件中取得陳述式開頭位移：  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* |-1 |預設  
表示資料列於其批次或保存物件的文字中描述之查詢的結束位置 (以位元組為單位)。  
  
*statement_start_offset*為**int**。  
  
-1 值代表批次的結尾。 預設值為-1。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|當編譯對應於這個計畫的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，作用中內容資料庫的識別碼。 對於隨選和準備的 SQL 陳述式而言，則為編譯陳述式的資料庫識別碼。<br /><br /> 資料行可為 Null。|  
|**objectid**|**int**|這個查詢計畫的物件識別碼 (如預存程序或使用者自訂函數)。 若是臨機操作和備妥的批次，這個資料行是**null**。<br /><br /> 資料行可為 Null。|  
|**number**|**smallint**|編號預存程序整數。 例如， **orders**應用程式的一組程式可以命名為**orderproc; 1**、 **orderproc; 2**，依此類推。 若是臨機操作和備妥的批次，這個資料行是**null**。<br /><br /> 資料行可為 Null。|  
|**加密**|**bit**|指出對應的預存程序是否加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 加密<br /><br /> 資料行不可為 Null。|  
|**query_plan**|**nvarchar(max)**|包含以*plan_handle*指定之查詢執行計畫的編譯時間顯示計畫標記法。 顯示計畫是文字格式。 每個包含諸如特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、預存程序呼叫和使用者自訂函數呼叫的批次，都會產生一份計畫。<br /><br /> 資料行可為 Null。|  
  
## <a name="remarks"></a>Remarks  
 在下列情況下，系統會在傳回的資料表之**plan**資料行中傳回「執行程式表」輸出**dm_exec_text_query_plan**：  
  
-   如果已從計畫快取中收回使用*plan_handle*所指定的查詢計劃，傳回資料表的**query_plan**資料行就是 null。 例如，如果已捕捉到計畫控制碼的時間，以及搭配使用**dm_exec_text_query_plan**，就會發生這個狀況。  
  
-   某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句不會進行快取，例如大量作業語句或包含大小超過 8 KB 之字串常值的語句。 這類語句的執行程式表無法使用**dm_exec_text_query_plan sys.databases**抓取，因為它們不存在於快取中。  
  
-   如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次或預存套裝程式含對使用者自訂函數的呼叫或動態 SQL 的呼叫（例如使用 EXEC （*string*）），則該使用者定義函數的已編譯 XML 執行程式表不會包含在針對批次或預存程式所傳回的資料表中， **dm_exec_text_query_plan** 。 相反地，您必須針對對應至使用者定義函數的*plan_handle* ，個別呼叫**dm_exec_text_query_plan** 。  
  
當臨機操作查詢使用[簡單](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)或[強制參數](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)化時，[ **query_plan** ] 資料行只會包含語句文字，而非實際的查詢計劃。 若要傳回查詢計劃，請呼叫**sys. dm_exec_text_query_plan** ，以取得備妥之參數化查詢的計畫控制碼。 您可以藉由參考[syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) view 的**sql**資料行或[sys.databases dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)動態管理檢視的文字資料行，判斷查詢是否已參數化。  
  
## <a name="permissions"></a>Permissions  
 若要執行**sys.databases dm_exec_text_query_plan**，使用者必須是**系統管理員（sysadmin** ）固定伺服器角色的成員，或具有伺服器的 VIEW server STATE 許可權。  
  
## <a name="examples"></a>範例  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 擷取執行緩慢的 Transact-SQL 查詢或批次之快取查詢計畫  
 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或批次在特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接上執行了很長一段時間，請擷取這項查詢或批次的執行計畫來找出延遲的原因。 下列範例會顯示如何針對執行緩慢的查詢或批次擷取顯示計畫。  
  
> [!NOTE]  
> 若要執行此範例，請將*session_id*和*plan_handle*的值取代為您的伺服器特定的值。  
  
 首先，請利用 `sp_who` 預存程序來擷取正在執行查詢或批次之處理序的伺服器處理序識別碼 (SPID)：  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 `sp_who` 傳回的結果集指出 SPID 是 `54`。 您可以搭配 `sys.dm_exec_requests` 動態管理檢視來使用 SPID，以利用下列查詢來擷取計畫控制代碼：  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 Sys 傳回的資料表**dm_exec_requests**表示執行緩慢的查詢或批次的計畫控制碼已 `0x06000100A27E7C1FA821B10600`。 下列範例會傳回指定計畫控制代碼的查詢計畫，並使用預設值 0 和 -1 傳回查詢或批次中的所有陳述式。  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>b. 從計畫快取中擷取每份查詢計畫  
 若要擷取計畫快取中所有查詢計畫的快照集，請查詢 `sys.dm_exec_cached_plans` 動態管理檢視，來擷取快取中所有查詢計畫的計畫控制代碼。 計畫控制代碼會儲存在 `plan_handle` 的 `sys.dm_exec_cached_plans` 資料行中。 之後，請依照下列方式，利用 CROSS APPLY 運算子，將計畫控制代碼傳給 `sys.dm_exec_text_query_plan`。 目前在計畫快取中的每個計畫的顯示計畫輸出，都是在傳回之資料表的 [`query_plan`] 資料行中。  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. 擷取伺服器已從計畫快取中收集了查詢統計資料的每項查詢計畫  
 若要擷取伺服器已收集了目前在計畫快取中的統計資料之所有查詢計畫的快照集，請查詢 `sys.dm_exec_query_stats` 動態管理檢視，以擷取快取中這些計畫的計畫控制代碼。 計畫控制代碼會儲存在 `plan_handle` 的 `sys.dm_exec_query_stats` 資料行中。 之後，請依照下列方式，利用 CROSS APPLY 運算子，將計畫控制代碼傳給 `sys.dm_exec_text_query_plan`。 每個計畫的顯示計畫輸出都在所傳回資料表的 `query_plan` 資料行中。  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 擷取按平均 CPU 時間排列之前五項查詢的相關資訊  
 下列範例會傳回前五項查詢的查詢計畫和平均 CPU 時間。 **Dm_exec_text_query_plan**函數會指定預設值0和-1，以傳回查詢計劃中批次的所有語句。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys. dm_exec_query_plan &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
