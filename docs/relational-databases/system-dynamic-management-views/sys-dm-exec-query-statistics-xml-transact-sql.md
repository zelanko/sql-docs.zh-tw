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
manager: craigg
ms.openlocfilehash: e5cb0bdbbbb535293835a0114061d8ca322ec8a8
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675097"
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
|sql_handle|**varbinary(64)**|要求的 SQL 文字雜湊對應。 可為 Null。|
|plan_handle|**varbinary(64)**|查詢計畫雜湊對應。 可為 Null。|
|query_plan|**xml**|執行程序表 XML 部分的統計資料。 可為 Null。|

## <a name="remarks"></a>備註
這個系統函數可從[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1。

這個系統函數的運作方式之下同時**標準**並**輕量級**查詢分析基礎結構的執行統計資料。  
  
**標準**可以藉由啟用分析基礎結構的統計資料：
  -  [在 SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md)
  -  [設定上的統計資料設定檔](../../t-sql/statements/set-statistics-profile-transact-sql.md)
  -  `query_post_execution_showplan`擴充的事件。  
  
**輕量型**分析基礎結構的統計資料可用於[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，可啟用：
  -  全域使用追蹤旗標 7412。
  -  使用[ *query_thread_profile* ](https://support.microsoft.com/kb/3170113)擴充的事件。
  
> [!NOTE]
> 一旦啟用追蹤旗標 7412、 輕量型程式碼剖析將會啟用分析基礎結構，而不是標準的分析，例如 DMV 查詢執行統計資料的任何消費者[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)。
> 不過，標準的程式碼剖析仍然使用 SET STATISTICS XML*包含實際的計劃*中的動作[!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]，和`query_post_execution_showplan`xEvent。

> [!IMPORTANT]
> TPC C 等工作負載測試，在啟用輕量型統計資料的分析基礎結構會加入到 1.5 到 2 個百分比的額外負荷。 相反地，標準的統計資料的分析基礎結構可以新增最多 90%的相同工作負載案例的額外負荷。

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

