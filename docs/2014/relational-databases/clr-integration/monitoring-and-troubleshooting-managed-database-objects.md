---
title: 監視和疑難排解 Managed 資料庫物件 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- monitoring [CLR integration]
- performance [CLR integration]
ms.assetid: a7b589ac-104d-4b68-b4aa-9f5fc192b13d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f03266a5460e9e34a404256e5df415f799b29d98
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090648"
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>監視與疑難排解 Managed 資料庫物件
  本主題提供可用於監視和疑難排解 Managed 資料庫物件以及在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中執行之組件的工具相關資訊。  
  
## <a name="profiler-trace-events"></a>Profiler 追蹤事件  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供 SQL 追蹤與事件通知，可監視 Database Engine 中所發生的事件。 SQL 追蹤可記錄指定的事件，藉以協助您進行效能的疑難排解、稽核資料庫活動、收集測試環境的範本資料、為 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式與預存程序偵錯，以及收集效能分析工具的資料等。 如需詳細資訊，請參閱 < [SQL 追蹤](../sql-trace/sql-trace.md)並[擴充事件](../extended-events/extended-events.md)。  
  
|事件|描述|  
|-----------|-----------------|  
|[Assembly Load 事件類別](../../database-engine/assembly-load-event-class.md)|用於監視組件載入要求 (成功或失敗)。|  
|[Sql: batchstarting 事件類別](../event-classes/sql-batchstarting-event-class.md)， [sql: batchcompleted 事件類別](../event-classes/sql-batchcompleted-event-class.md)|提供已啟動或已完成之 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 批次的相關資訊。|  
|[SP: Starting 事件類別](../event-classes/sp-starting-event-class.md)， [SP: Completed 事件類別](../event-classes/sp-completed-event-class.md)|用於監視 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 預存程序的執行。|  
|[Sql: stmtstarting 事件類別](../event-classes/sql-stmtstarting-event-class.md)， [sql: stmtcompleted 事件類別](../event-classes/sql-stmtcompleted-event-class.md)|用於監視 CLR 和 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 常式的執行。|  
  
## <a name="performance-counters"></a>效能計數器  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 所提供的物件與計數器，可供「系統監視器」用來對執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的電腦監視其中的活動。 物件可以是任何一種 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資源，例如 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 鎖定或 Windows 處理序。 每個物件都包含一個或多個計數器，可決定欲監視之物件的不同層面。 如需詳細資訊，請參閱 [使用 SQL Server 物件](../performance-monitor/use-sql-server-objects.md)。  
  
|Object|描述|  
|------------|-----------------|  
|[SQL Server 的 CLR 物件](../performance-monitor/sql-server-clr-object.md)|執行 CLR 所花費的全部時間。|  
  
## <a name="windows-system-monitor-perfmonexe-counters"></a>Windows 系統監視器 (PERFMON.EXE) 計數器  
 Windows 系統監視器 (PERFMON.EXE) 工具包含數個可用於監視 CLR 整合應用程式的效能計數器。 .NET CLR 效能計數器可以透過 "sqlservr" 處理序名稱進行篩選，以追蹤目前正在執行的 CLR 整合應用程式。  
  
|效能物件|描述|  
|------------------------|-----------------|  
|SqlServer:CLR|提供伺服器的 CPU 統計資料。|  
|.NET CLR 例外狀況|追蹤每秒的例外狀況數目。|  
|.NET CLR 載入|提供載入到伺服器中之 AppDomains 和組件的相關資訊。|  
|.NET CLR 記憶體|提供 CLR 記憶體使用量的相關資訊。 如果記憶體使用量變得太大，可以使用此物件來標示警示。|  
|.NET Data Provider for SQL Server|追蹤每秒的連接數目和中斷連接數目。 此物件可用於監視資料庫活動的層級。|  
  
## <a name="catalog-views"></a>目錄檢視  
 目錄檢視會傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Database Engine 所使用的資訊。 建議您使用目錄檢視，因為它們是目錄中繼資料最一般性的介面，提供了取得、轉換和呈現這項資訊之自訂形式的最有效方法。 所有使用者能夠使用的目錄中繼資料都是利用目錄檢視公開的。 如需詳細資訊，請參閱[目錄檢視 &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)。  
  
|目錄檢視|描述|  
|------------------|-----------------|  
|[sys.assemblies &#40;Transact SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)|傳回資料庫中註冊之組件的相關資訊。|  
|[sys.assembly_references &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)|識別參考其他組件的組件。|  
|[sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)|傳回組件中所定義之每個函數、預存程序與觸發程序的相關資訊。|  
|[sys.assembly_files &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)|傳回資料庫中註冊之組件檔案的相關資訊。|  
|[sys.assembly_types &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)|識別組件所定義的使用者定義型別 (UDT)。|  
|[sys.module_assembly_usages &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql)|識別在其中定義 CLR 模組的組件。|  
|[sys.parameter_type_usages &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql)|傳回使用者定義型別之參數的相關資訊。|  
|[sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)|識別在其中定義 CLR 觸發程序的組件。|  
|[sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)|識別伺服器上的伺服器層級 DDL 觸發程序，包括 CLR 觸發程序。|  
|[sys.type_assembly_usages &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql)|識別在其中定義使用者定義型別的組件。|  
|[sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)|傳回資料庫中註冊的系統爛使用者定義型別。|  
  
## <a name="dynamic-management-views"></a>動態管理檢視  
 動態管理檢視和函數傳回伺服器狀態資訊，這項資訊可用來監視伺服器執行個體的健全狀況、診斷問題和調整效能。 如需詳細資訊，請參閱 <<c0> [ 動態管理檢視和函式&#40;TRANSACT-SQL&#41;](../views/views.md)。</c0>  
  
|DMV|描述|  
|---------|-----------------|  
|[sys.dm_clr_appdomains &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql)|提供伺服器中每個應用程式網域的相關資訊。|  
|[sys.dm_clr_loaded_assemblies &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql)|識別伺服器上註冊的每個 Managed 組件。|  
|[sys.dm_clr_properties &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql)|傳回主控 CLR 的相關資訊。|  
|[sys.dm_clr_tasks &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql)|識別目前正在執行的所有 CLR 工作。|  
|[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)|傳回 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 快取的查詢執行計畫相關資訊，讓查詢執行更快速。|  
|[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)|傳回快取查詢計畫的彙總效能統計資料。|  
|[sys.dm_exec_requests &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql)|傳回在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中執行之每項要求的相關資訊。|  
|[sys.dm_os_memory_clerks &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql)|傳回目前在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體作用中的所有記憶體 Clerk，包括 CLR 記憶體 Clerk。|  
  
## <a name="see-also"></a>另請參閱  
 [Common Language Runtime &#40;CLR&#41; 整合程式設計概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
