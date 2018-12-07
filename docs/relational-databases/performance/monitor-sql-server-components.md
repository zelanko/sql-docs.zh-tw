---
title: 監視 SQL Server 元件 | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: e8f1b16b-ea40-4e12-886c-967ebda4e6e4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22f618072cb9e8636e3fef59d4ee7513033229d6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527497"
---
# <a name="monitor-sql-server-components"></a>監視 SQL Server 元件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是在動態環境下提供服務，所以監視很重要。 應用程式中的資料會變更。 使用者需要的存取類型會變更。 使用者的連接方式會變更。 甚至存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的應用程式類型也可能變更，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動管理系統層級的資源，例如記憶體和磁碟空間，以便將系統層級的密集手動微調需求降到最低。 監視可讓管理員識別效能趨勢，以決定是否需要變更。  
  
若要有效監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何元件：  
  
1.  決定您的監視目標。  
2.  選取適當的工具。    
3.  識別要監視的元件。  
4.  選取這些元件的標準。  
5.  監視伺服器。  
6.  分析資料。  
  
以下依次討論這些步驟。  
  
## <a name="determine-your-monitoring-goals"></a>決定您的監視目標  
若要有效監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您應該具體描述您的監視理由。 可以包括下列理由：  
  
-   建立效能基準線。  
-   識別效能變更趨勢。  
-   診斷特定效能問題。  
-   識別要最佳化的元件或處理序。  
-   比較不同用戶端應用程式在效能上的影響。  
-   稽核使用者活動。  
-   以不同的負載來測試伺服器。  
-   測試資料庫架構。  
-   測試維護排程。  
-   測試備份與還原計畫。  
-   決定修改硬體組態的時間。  
  
## <a name="select-the-appropriate-tool"></a>選取適當的工具  
決定監視的原因之後，您應該針對該監視類型選取適當的工具。 Windows 作業系統和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供完整的工具集合，可在交易密集的環境中監視伺服器。 這些工具可清楚地呈現 SQL Server Database Engine 執行個體或 SQL Server Analysis Services 執行個體的狀況。  
  
Windows 會提供下列工具來監視伺服器上執行的應用程式：  
  
-   [系統監視器](../../relational-databases/performance/start-system-monitor-windows.md)，可讓您收集和檢視記憶體、磁碟及處理器用量等活動的即時資料。  
-   效能記錄與警示  
-   工作管理員  
  
如需有關 Windows Server 或 Windows 工具的詳細資訊，請參閱 Windows 文件集。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可提供下列工具來監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的元件：  
  
-   [擴充事件](../../relational-databases/extended-events/extended-events.md)
-   [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
-   [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
-   [Distributed Replay Utility](../../tools/distributed-replay/sql-server-distributed-replay.md)  
-   [活動監視器](../../relational-databases/performance-monitor/activity-monitor.md)  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 圖形化顯示計畫  
-   [系統預存程序](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
-   [資料庫主控台命令 (DBCC)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
-   [動態管理檢視和函數](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
-   [函數](../../t-sql/functions/functions.md)   
-   [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)   

> [!IMPORTANT]
> 已淘汰 SQL 追蹤和 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]。 也已淘汰包含 Microsoft SQL Server 追蹤和重新執行物件的 *Microsoft.SqlServer.Management.Trace* 命名空間。 
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 
> 請改用擴充事件。 如需[擴充事件](../../relational-databases/extended-events/extended-events.md)的詳細資訊，請參閱[快速入門︰SQL Server 中的擴充事件](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)和 [SSMS XEvent 分析工具](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md)。

> [!NOTE]
> 「未」淘汰適用於 Analysis Services 工作負載的 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，而且將會繼續受支援。

如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監視工具的詳細資訊，請參閱 [效能監視及微調工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)。  
  
## <a name="identify-the-components-to-monitor"></a>識別要監視的元件  
監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的第三個步驟是識別您監視的元件。 例如，如果使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來追蹤伺服器，您可以定義追蹤來收集特定事件的資料。 您也可以排除不符合情況的事件。  
  
## <a name="select-metrics-for-monitored-components"></a>選取受監視元件的標準  
識別要監視的元件之後，請決定您監視的元件標準。 例如，選取要納入追蹤的事件之後，您可以選擇只包含事件的特定資料。 將追蹤限制在與追蹤相關的資料上，可以將執行追蹤所需的系統資源減到最小。  
  
## <a name="monitor-the-server"></a>監視伺服器  
若要監視伺服器，請執行您已設定來蒐集資料的監視工具。 例如，定義追蹤之後，您可以執行追蹤來蒐集伺服器中所引發的事件之相關資料。  

## <a name="analyze-the-data"></a>分析資料  
完成追蹤之後，請分析資料，以查看是否已達到您的監視目標。 如果尚未達成，請修改您用來監視伺服器的元件或標準。  
  
以下概略說明擷取與使用事件資料的程序。  
  
1.  套用篩選來限制要收集的事件資料。  
  
    限制事件資料可讓系統把焦點放在監視案例相關的事件上。 例如，若您要監視慢速查詢，可以使用篩選來限制只監視應用程式對特定資料庫執行超過三十秒以上的查詢。 
    
    如需篩選擴充事件追蹤的詳細資訊，請參閱[快速入門︰SQL Server 中的擴充事件](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md#demo-of-ssms-integration)。 
    
    如需篩選 SQL 追蹤的詳細資訊，請參閱[設定追蹤篩選 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md) 和[篩選追蹤中的事件 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)。  
  
2.  監視 (擷取) 事件。  
  
    一旦啟用後，使用中的監視會從指定的應用程式、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體或作業系統中擷取資料。 例如，使用「系統監視器」監視磁碟活動時，監視會擷取磁碟讀寫動作等事件資料，並顯示在螢幕上。 如需詳細資訊，請參閱[監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)。  
  
3.  儲存擷取的事件資料。  
  
    儲存擷取的事件資料，可讓您稍後再分析它。 您可將擷取的事件資料儲存到檔案，而檔案可以重新載入到原先建立該檔案的工具中，以進行分析。 在建立效能基準時，儲存擷取的事件資料就很重要。 效能基準資料會儲存起來，並在比較最近擷取的事件資料時使用，以判斷效能是否為最佳化。
    
    擴充事件允許將事件資料儲存到事件檔案、事件計數器、長條圖和信號緩衝區。 如需詳細資訊，請參閱 [SQL Server 中的擴充事件目標](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md)。
    
    SQL 追蹤事件資料可以使用 Distributed Replay Utility 或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來重新執行。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 允許將事件資料儲存到檔案或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 如需詳細資訊，請參閱 [SQL Server Profiler 範本和權限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)。  
  
4.  建立包含指定設定的追蹤範本來擷取事件。  
  
    追蹤範本中包含事件本身、事件資料和用來擷取資料的篩選等相關規格。 這些範本稍後可以用來監視特定的事件組合，而不需重新定義事件、事件資料與篩選。 例如，如果您要時常監視死結的數目與陷入死結的使用者數目，您可以建立一個定義這些事件、事件資料與事件篩選的範本、儲存範本，然後在下次要監視死結時重新套用此篩選。
    
    擴充事件工作階段定義是可撰寫指令碼且可重複使用的範本。 若要建立及管理工作階段，請參閱[在物件總管中管理事件工作階段](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)。 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] XEvent Profiler 已提供可立即使用的範本。 如需詳細資訊，請參閱[使用 SSMS XEvent 分析工具](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md)。
       
    [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 會針對這個目的使用追蹤範本。 如需詳細資訊，請參閱[設定追蹤定義預設值 &#40;SQL Server Profiler & #41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md) 和[建立追蹤範本 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md)。  
    
    > [!TIP]
    > SQL 追蹤定義可以轉換成擴充事件工作階段。 如需詳細資訊，請參閱[將現有的 SQL 追蹤指令碼轉換為擴充事件工作階段](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)。
  
5.  分析擷取的事件資料。  
  
     為了進行分析，擷取的事件資料會載入擷取資料的應用程式中。 
     
     例如，您可以將擷取的擴充事件追蹤重新載入至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以進行檢視及分析。 如需詳細資訊，請參閱 [進階檢視 SQL Server 中擴充事件的目標資料](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)。

     您可以將 SQL 追蹤資料重新載入至 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 中，以進行檢視及分析。 如需詳細資訊，請參閱 [使用 SQL Server Profiler 檢視和分析追蹤](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)。  
  
     分析事件資料涉及判斷發生何事與發生的原因。 這項資訊可讓您利用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或預存程序等 (視執行的分析類型而定)，執行變更以改善效能，例如增加更多記憶體、變更索引、修正程式碼問題。 例如，您可以使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 來分析從擴充的事件或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 擷取的追蹤，並根據結果提供索引建議。  
  
6.  重新執行擷取的事件資料 (選擇性)。  
  
     事件重新執行可讓您仿造原先擷取資料的資料庫環境來建立測試副本，然後模擬原本發生在實際系統的狀況來重複執行擷取的事件。 只有 Distributed Replay Utility 或 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]提供這項功能。 您可以使用原本的發生速度、盡量加快 (用以驅策系統) 或甚至一次一個步驟來重新執行這些事件，以便在發生每個事件之後分析系統。 藉由在測試環境下分析確實的事件，可以避免損害實際系統。 如需詳細資訊，請參閱 [重新執行追蹤](../../tools/sql-server-profiler/replay-traces.md)。  
  
  
