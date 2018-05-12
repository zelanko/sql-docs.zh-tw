---
title: 監視 Analysis Services with SQL Server Profiler 簡介 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7b3c2dcec84956cd83c09a6c9be1d70975df67cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>使用 SQL Server Profiler 監視 Analysis Services 簡介
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  您可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來監視由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體產生的事件。 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以執行下列動作：  
  
-   監視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的效能。  
  
-   偵錯多維度運算式 (MDX) 陳述式。  
  
-   識別執行緩慢的 MDX 陳述式。  
  
-   在專案的開發階段透過逐步執行陳述式來測試 MDX 陳述式，以確認程式碼如預期般運作。  
  
-   藉由在測試系統上重新執行於實際系統上擷取到的事件，即可在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中進行問題的疑難排解。 此方式對測試或偵錯用途很有用，並可讓使用者不受干擾的繼續使用實際系統。  
  
-   發生在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體上的稽核和檢閱活動。 安全性管理員可以檢閱任何一個稽核的事件。 這包含登入嘗試是成功或失敗；以及存取陳述式和物件的權限是成功或失敗。  
  
-   在螢幕上顯示有關擷取事件的資料，或擷取有關每個事件的資料並儲存到檔案或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，以供未來分析或播放使用。 當您重新執行資料時，可以即時或逐步返回儲存的事件，如同最初發生時一般。  
  
## <a name="using-sql-server-profiler"></a>使用 SQL Server Profiler  
 若要使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來建立或重新執行追蹤，您必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器角色的成員。 如果您是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器角色的成員，就可以從 [開始] 功能表上的 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] 程式集啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 當您使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 時，請注意下列事項：  
  
-   追蹤定義會使用 CREATE 陳述式與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫一同儲存。  
  
-   可以同時執行多個追蹤。  
  
-   多重連接可以從相同的追蹤接收事件。  
  
-   當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 停止並重新啟動時，追蹤可以繼續執行。  
  
    > [!NOTE]  
    >  追蹤事件中不會顯示密碼，而是以 ****** 取代。  
  
 為了達到最佳效能，請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 只監視您需要的事件。 監視太多事件會增加負擔，並導致追蹤檔案或資料表變得過於龐大，尤其在進行長期追蹤時。 另外，請使用篩選來限制收集的資料量，以防止追蹤檔案變得太大。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](../../analysis-services/trace-events/analysis-services-trace-events.md)   
 [建立 Profiler 追蹤以重新顯示 & #40;Analysis Services & #41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md)  
  
  
