---
title: sys.dm_exec_sql_text (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_sql_text
- sys.dm_exec_sql_text
- sys.dm_exec_sql_text_TSQL
- dm_exec_sql_text_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sql_text dynamic management function
ms.assetid: 61b8ad6a-bf80-490c-92db-58dfdff22a24
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6c6d65221afc0e9f6967d944c137693311c31c84
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmexecsqltext-transact-sql"></a>sys.dm_exec_sql_text (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  也就是批次的 SQL 文字傳回識別指定*sql_handle*。 這個資料表值函式取代系統函數**fn_get_sql**。  
  
 
## <a name="syntax"></a>語法  
  
```  
sys.dm_exec_sql_text(sql_handle | plan_handle)  
```  
  
## <a name="arguments"></a>引數  
*sql_handle*  
這是要查閱之批次的 SQL 控制代碼。 *sql_handle*是**varbinary(64)**。 *sql_handle*可以從下列動態管理物件取得：  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)  
  
-   [sys.dm_exec_xml_handles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)  
  
-   [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  
  
*plan_handle*  
用來唯一識別批次的查詢計畫，該批次可能已快取或正在執行。 *plan_handle*是**varbinary(64)**。 *plan_handle*可以從下列動態管理物件取得：  
  
-   [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|資料庫的識別碼。<br /><br /> 對於隨選和準備的 SQL 陳述式而言，則為編譯陳述式的資料庫識別碼。|  
|**objectid**|**int**|物件的識別碼。<br /><br /> 特定和準備 SQL 陳述式的這個值是 NULL。|  
|**number**|**smallint**|對於已編號的預存程序，這個資料行會傳回預存程序的編號。 如需詳細資訊，請參閱[之 deprecated sys.numbered_procedures &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)。<br /><br /> 特定和準備 SQL 陳述式的這個值是 NULL。|  
|**加密**|**bit**|1 = SQL 文字已加密。<br /><br /> 0 = SQL 文字未加密。|  
|**text**|**nvarchar(max** **)**|SQL 查詢的文字。<br /><br /> 加密物件的這個值是 NULL。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 `VIEW SERVER STATE` 權限。  
  
## <a name="remarks"></a>備註  
對於臨機操作查詢，SQL 控制代碼是依據提交給伺服器的 SQL 文字的雜湊值，並可以來自於任何資料庫。 

針對預存程序、觸發程序或函數之類的資料庫物件，SQL 控制代碼是從資料庫識別碼、物件識別碼和物件編碼衍生而來。 

計畫控制代碼是從整個批次的已編譯計畫衍生的雜湊值。 

> [!NOTE]
> **dbid**無法由*sql_handle*臨機操作查詢。 若要判斷**dbid**臨機操作查詢，使用*plan_handle*改為。
  
## <a name="examples"></a>範例 

### <a name="a-conceptual-example"></a>A. 概念的範例
以下是一個基本範例，說明傳遞**sql_handle**直接或使用**CROSS APPLY**。
  1.  建立活動。  
在新的 [查詢] 視窗中執行下列 T-SQL [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。   
      ```sql
      -- Identify current spid (session_id)
      SELECT @@SPID;
      GO
  
      -- Create activity
        WAITFOR DELAY '00:02:00';
      ```
      
    2.  使用**CROSS APPLY**。  
    從 sql_handle **sys.dm_exec_requests**會傳遞至**sys.dm_exec_sql_text**使用**CROSS APPLY**。 開啟新的查詢視窗，並傳遞步驟 1 所識別的 spid。 在此範例中的 spid 剛好是`59`。

        ```sql
        SELECT t.*
        FROM sys.dm_exec_requests AS r
        CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t
        WHERE session_id = 59 -- modify this value with your actual spid
         ```      
 
    2.  傳遞**sql_handle**直接。  
取得**sql_handle**從**sys.dm_exec_requests**。 然後，傳遞**sql_handle**直接**sys.dm_exec_sql_text**。 開啟新查詢視窗，並傳遞步驟 1 中所識別的 spid **sys.dm_exec_requests**。 在此範例中的 spid 剛好是`59`。 接著，將傳回**sql_handle**做為引數**sys.dm_exec_sql_text**。

        ```sql
        -- acquire sql_handle
        SELECT sql_handle FROM sys.dm_exec_requests WHERE session_id = 59  -- modify this value with your actual spid
        
        -- pass sql_handle to sys.dm_exec_sql_text
        SELECT * FROM sys.dm_exec_sql_text(0x01000600B74C2A1300D2582A2100000000000000000000000000000000000000000000000000000000000000) -- modify this value with your actual sql_handle
         ```      
    
  
### <a name="b-obtain-information-about-the-top-five-queries-by-average-cpu-time"></a>B. 取得前五項查詢的平均 CPU 時間資訊  
 下列範例會傳回 SQL 陳述式的文字以及前五項查詢的平均 CPU 時間。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
    SUBSTRING(st.text, (qs.statement_start_offset/2)+1,   
        ((CASE qs.statement_end_offset  
          WHEN -1 THEN DATALENGTH(st.text)  
         ELSE qs.statement_end_offset  
         END - qs.statement_start_offset)/2) + 1) AS statement_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
ORDER BY total_worker_time/execution_count DESC;  
```  
  
### <a name="c-provide-batch-execution-statistics"></a>C. 提供批次執行統計資料  
 下列範例會傳回以批次方式執行的 SQL 查詢之文字並提供有關這些查詢的統計資訊。  
  
```sql  
SELECT s2.dbid,   
    s1.sql_handle,    
    (SELECT TOP 1 SUBSTRING(s2.text,statement_start_offset / 2+1 ,   
      ( (CASE WHEN statement_end_offset = -1   
         THEN (LEN(CONVERT(nvarchar(max),s2.text)) * 2)   
         ELSE statement_end_offset END)  - statement_start_offset) / 2+1))  AS sql_statement,  
    execution_count,   
    plan_generation_num,   
    last_execution_time,     
    total_worker_time,   
    last_worker_time,   
    min_worker_time,   
    max_worker_time,  
    total_physical_reads,   
    last_physical_reads,   
    min_physical_reads,    
    max_physical_reads,    
    total_logical_writes,   
    last_logical_writes,   
    min_logical_writes,   
    max_logical_writes    
FROM sys.dm_exec_query_stats AS s1   
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS s2    
WHERE s2.objectid is null   
ORDER BY s1.sql_handle, s1.statement_start_offset, s1.statement_end_offset;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_cursors &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)   
 [sys.dm_exec_xml_handles &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [使用 [套用]](../../t-sql/queries/from-transact-sql.md#using-apply)   
 [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  

