---
title: 使用 SQL Server Profiler 監視 Analysis Services 簡介 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 568ec549-5ddc-493a-b9f8-3bdc548b562e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3146f5a9f3e22753cc86c07b609d997be580b9f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079800"
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>使用 SQL Server Profiler 監視 Analysis Services 簡介
  您可以使用[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]來監視由實例產生的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]事件。 使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以執行下列動作：  
  
-   監視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體的效能。  
  
-   偵錯多維度運算式 (MDX) 陳述式。  
  
-   識別執行緩慢的 MDX 陳述式。  
  
-   在專案的開發階段透過逐步執行陳述式來測試 MDX 陳述式，以確認程式碼如預期般運作。  
  
-   藉由在測試系統上重新執行於實際系統上擷取到的事件，即可在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中進行問題的疑難排解。 此方式對測試或偵錯用途很有用，並可讓使用者不受干擾的繼續使用實際系統。  
  
-   發生在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體上的稽核和檢閱活動。 安全性管理員可以檢閱任何一個稽核的事件。 這包含登入嘗試是成功或失敗；以及存取陳述式和物件的權限是成功或失敗。  
  
-   在螢幕上顯示有關擷取事件的資料，或擷取有關每個事件的資料並儲存到檔案或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中，以供未來分析或播放使用。 當您重新執行資料時，可以即時或逐步返回儲存的事件，如同最初發生時一般。  
  
## <a name="using-sql-server-profiler"></a>使用 SQL Server Profiler  
 若要使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來建立或重新執行追蹤，您必須是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器角色的成員。 如果您是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器角色的成員，就可以從 [開始]**** 功能表上的 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 程式集啟動 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 當您使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]時，請注意下列事項：  
  
-   追蹤定義會使用 CREATE 陳述式與 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫一同儲存。  
  
-   可以同時執行多個追蹤。  
  
-   多重連接可以從相同的追蹤接收事件。  
  
-   當 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 停止並重新啟動時，追蹤可以繼續執行。  
  
    > [!NOTE]  
    >  追蹤事件中不會顯示密碼，但會\* \* \* \* \* \*在事件中取代。  
  
 為了達到最佳效能，請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 只監視您需要的事件。 監視太多事件會增加負擔，並導致追蹤檔案或資料表變得過於龐大，尤其在進行長期追蹤時。 另外，請使用篩選來限制收集的資料量，以防止追蹤檔案變得太大。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 追蹤事件](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [建立 Profiler 追蹤以重新執行 &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md)  
  
  
