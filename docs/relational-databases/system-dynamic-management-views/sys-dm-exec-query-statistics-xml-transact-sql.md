---
title: sys.dm_exec_query_statistics_xml (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 06091ffc26ea036a4a0bd7e30196545bcaca60d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936940"
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

傳回查詢執行計畫進行中的要求。 您可以使用此 DMV 來擷取 showplan XML 暫時性統計資料。 

## <a name="syntax"></a>語法

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>引數 
*session_id*  
 執行要查閱之批次的工作階段識別碼。 *session_id*已**smallint**。 *session_id*可以從下列動態管理物件取得：  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>傳回的資料表

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|工作階段的識別碼。 不可為 Null。|
|request_id|**int**|要求的識別碼。 不可為 Null。|
|sql_handle|**varbinary(64)**|語彙基元，可唯一識別批次或預存程序查詢的一部分。 可為 Null。|
|plan_handle|**varbinary(64)**|是可唯一識別目前正在執行的批次的查詢執行計劃權杖。 可為 Null。|
|query_plan|**xml**|包含執行階段查詢執行計畫所指定的顯示計畫表示法*plan_handle*包含部分的統計資料。 顯示計畫是 XML 格式。 每個包含諸如特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、預存程序呼叫和使用者自訂函數呼叫的批次，都會產生一份計畫。 可為 Null。|

## <a name="remarks"></a>備註
這個系統函數可從[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1。 請參閱知識庫[3190871](https://support.microsoft.com/en-us/help/3190871)

這個系統函數的運作方式之下同時**標準**並**輕量級**查詢分析基礎結構的執行統計資料。 如需詳細資訊，請參閱[查詢分析基礎結構](../../relational-databases/performance/query-profiling-infrastructure.md)。  

在下列情況中，任何顯示計畫輸出都會傳入**query_plan**傳回之資料表的資料行**sys.dm_exec_query_statistics_xml**:  
  
-   如果查詢計畫，對應於指定*session_id*不會再執行**query_plan**傳回之資料表的資料行是 null。 比方說，如果沒有時擷取計畫控制代碼，以及當它搭配之間的時間延遲可能會發生這種情況**sys.dm_exec_query_statistics_xml**。  
    
基於中允許的巢狀層級數目的限制**xml**資料類型**sys.dm_exec_query_statistics_xml**無法傳回達到或超過 128 個層級的巢狀項目查詢計劃。 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這會讓查詢計畫無法傳回並產生錯誤 6335。 在  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 和更新版本中， **query_plan**資料行會傳回 NULL。   

## <a name="permissions"></a>Permissions  
 需要伺服器的 `VIEW SERVER STATE` 權限。  

## <a name="examples"></a>範例  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. 查看執行中批次的即時查詢計畫和執行統計資料  
 下列範例會查詢**sys.dm_exec_requests**來尋找有趣的查詢並複製其`session_id`從輸出中。  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 然後，若要取得即時查詢計畫和執行統計資料，請使用 複製`session_id`搭配系統函數**sys.dm_exec_query_statistics_xml**。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 或結合的所有執行的要求。  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>另請參閱
  [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [與資料庫相關動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

