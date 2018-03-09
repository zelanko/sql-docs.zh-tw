---
title: "使用預存程序建立手動追蹤 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-trace
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b66d79a0da8d29a96df3129edd7681558ed281c0
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="create-manual-traces-using-stored-procedures"></a>使用預存程序建立手動追蹤
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所提供的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統預存程序可建立 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體的追蹤。 您可以從自己的應用程式中使用這些系統預存程序以手動建立追蹤，而不是使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]建立追蹤。 如此一來，就可以依照您的企業需求撰寫自訂的應用程式。  
  
## <a name="in-this-section"></a>本節內容  
 下表列出用於追蹤 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]之執行個體的系統預存程序。  
  
|預存程序|已執行的工作|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)|傳回追蹤中所含事件的相關資訊。|  
|[sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)|傳回所指定追蹤或所有現有追蹤的資訊。|  
|[sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)|建立追蹤定義。 新追蹤會處於已停止狀態。|  
|[sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)|建立使用者定義事件。|  
|[sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)|在追蹤中新增或移除事件類別或資料行。|  
|[sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|啟動、停止或關閉追蹤。|  
|[sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)|傳回追蹤所套用之篩選的相關資訊。|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|將新的或修改過的篩選套用至追蹤。|  
  
 **若要使用預存程序來定義自己的追蹤**  
  
1.  使用 **sp_trace_setevent**指定要擷取的事件。  
  
2.  指定事件篩選條件。 如需詳細資訊，請參閱[設定追蹤篩選 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)。  
  
3.  使用 **sp_trace_create** 指定擷取事件資料的目的地。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
 **若要設定追蹤定義預設值**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
 **若要設定追蹤顯示預設值**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **若要建立追蹤**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
 **若要從追蹤範本中移除事件**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
