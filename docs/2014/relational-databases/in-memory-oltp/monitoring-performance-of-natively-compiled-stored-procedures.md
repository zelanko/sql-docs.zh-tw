---
title: 監視原生編譯預存程序的效能 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 55548cb2-77a8-4953-8b5a-f2778a4f13cf
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fa8a92b3727bf4c06a5b5a85c8359f96b592cd44
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359750"
---
# <a name="monitoring-performance-of-natively-compiled-stored-procedures"></a>監視原生編譯預存程序的效能
  本主題討論如何監視原生編譯預存程序的效能  
  
## <a name="using-extended-events"></a>使用擴充的事件  
 使用 `sp_statement_completed` 擴充事件來追蹤查詢的執行。 以此事件建立擴充事件工作階段，選擇性地針對特定原生編譯預存程序篩選 object_id。執行每項查詢之後都將引發此擴充事件。 擴充事件所報告的 CPU 時間和持續時間代表了查詢的 CPU 使用率和執行時間。 原生編譯預存程序若佔用大量的 CPU 時間，可能就會導致效能問題。  
  
 `line_number` 連同擴充事件中的 `object_id` 皆可用來調查查詢。 使用下列查詢即可擷取程序定義。 行號可用來識別定義內的查詢：  
  
```tsql  
select [definition] from sys.sql_modules where object_id=object_id  
```  
  
 如需詳細資訊`sp_statement_completed`擴充事件，請參閱[如何擷取導致事件的陳述式](https://blogs.msdn.com/b/extended_events/archive/2010/05/07/making-a-statement-how-to-retrieve-the-t-sql-statement-that-caused-an-event.aspx)。  
  
## <a name="using-data-management-views"></a>使用資料管理檢視  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援收集原生編譯預存程序在程序層級和查詢層級的執行統計資料。 收集執行統計資料會影響效能，所以預設並未啟用。  
  
 您可以使用 [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql) 啟用和停用原生編譯預存程序的統計資料收集。  
  
 使用 [sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql) 啟用統計資料收集時，您可以使用 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) 監視原生編譯預存程序的效能。  
  
 使用 [sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql) 啟用統計資料收集時，您可以使用 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql) 監視原生編譯預存程序的效能。  
  
 在一開始收集時，啟用統計資料集合。 接著，執行原生編譯預存程序。 在結束收集後，停用統計資料集合。 接著，分析 DMV 所傳回的執行統計資料。  
  
 收集統計資料之後，使用 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql) 和 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql) 分別可查詢原生編譯預存程序的程序層級和查詢層級執行統計資料。  
  
> [!NOTE]  
>  如果統計資料集合啟用的對象是原生編譯預存程序，則收集的工作者時間單位為毫秒。 若查詢的執行時間少於一毫秒，其值將會是 0。 如果原生編譯預存程序執行數次的時間都少於 1 毫秒， **total_worker_time** 可能就不準確。  
  
 下列查詢會在收集統計資料之後傳回目前資料庫中原生編譯預存程序的程序名稱和執行統計資料：  
  
```tsql  
select object_id,  
       object_name(object_id) as 'object name',  
       cached_time,  
       last_execution_time,  
       execution_count,  
       total_worker_time,  
       last_worker_time,  
       min_worker_time,  
       max_worker_time,  
       total_elapsed_time,  
       last_elapsed_time,  
       min_elapsed_time,  
       max_elapsed_time   
from sys.dm_exec_procedure_stats  
where database_id=db_id() and object_id in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by total_worker_time desc  
```  
  
 下列查詢會傳回目前資料庫中已收集統計資料的原生編譯預存程序內，所有查詢的查詢文字和執行統計資料，依工作者時間總計以遞減順序排序：  
  
```tsql  
select st.objectid,   
       object_name(st.objectid) as 'object name',   
       SUBSTRING(st.text, (qs.statement_start_offset/2) + 1, ((qs.statement_end_offset-qs.statement_start_offset)/2) + 1) as 'query text',   
       qs.creation_time,  
       qs.last_execution_time,  
       qs.execution_count,  
       qs.total_worker_time,  
       qs.last_worker_time,  
       qs.min_worker_time,  
       qs.max_worker_time,  
       qs.total_elapsed_time,  
       qs.last_elapsed_time,  
       qs.min_elapsed_time,  
       qs.max_elapsed_time  
from sys.dm_exec_query_stats qs cross apply sys.dm_exec_sql_text(sql_handle) st  
where  st.dbid=db_id() and st.objectid in (select object_id   
from sys.sql_modules where uses_native_compilation=1)  
order by qs.total_worker_time desc  
```  
  
 原生編譯預存程序支援 SHOWPLAN_XML (估計執行計畫)。 估計執行計畫可用來檢查查詢計劃，以找出任何的計劃錯誤問題。 計劃錯誤的常見原因包括：  
  
-   在建立程序之前未先更新統計資料。  
  
-   遺漏索引。  
  
 執行程序表 XML 可透過執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)]取得：  
  
```tsql  
SET SHOWPLAN_XML ON  
GO  
EXEC my_proc   
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 或者，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中選取程序名稱，然後按一下 **[顯示估計執行計畫]**。  
  
 原生編譯預存程序的估計執行計畫會顯示程序內各查詢的查詢運算子和運算式。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 並未支援原生編譯預存程序的所有 SHOWPLAN_XML 屬性。 例如，與查詢最佳化工具成本相關的屬性並未納入程序的 SHOWPLAN_XML。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)  
  
  
