---
title: 監視資源使用狀況 (系統監視器) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], resource usage
- System Monitor [SQL Server], about Windows System Monitor
- resource usage monitoring [SQL Server]
- System Monitor [SQL Server]
- counters [SQL Server], resource usage subjects
- performance counters [SQL Server], resource usage subjects
- Windows System Monitor [SQL Server], about Windows System Monitor
- monitoring [SQL Server], server resource usage
- monitoring resource usage [SQL Server]
- Windows System Monitor [SQL Server]
- database monitoring [SQL Server], resource usage
- database performance [SQL Server], resource usage
- tuning databases [SQL Server], resource usage
- server performance [SQL Server], resource usage
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8bd4676eed22cea99808d87016231dbd2ebaf4cc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777060"
---
# <a name="monitor-resource-usage-system-monitor"></a>監視資源使用狀況 (系統監視器)
  如果您正在執行 Microsoft Windows 伺服器作業系統，請使用系統監視器圖形工具，測量 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的效能。 您可以檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件、效能計數器及其他物件 (如處理器、記憶體、快取、執行緒和處理序) 的行為。 這些物件每一個都有一組關聯的計數器，可測量裝置的使用狀況 (Usage)、佇列長度 (Queue Length)、延遲 (Delay) 和產能 (Throughput) 及內部壅塞的其他指示器。  
  
> [!NOTE]  
>  在 Windows NT 4.0 之後，系統監視器已取代效能監視器。  
  
## <a name="benefits-of-system-monitor"></a>系統監視器的優點  
 系統監視器可同時監視 Windows 作業系統與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 計數器，有助於判斷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 Windows 的效能之間是否有任何關聯。 例如，同時監視 Windows 磁碟輸入/輸出 (I/O) 計數器與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 緩衝區管理員計數器，可顯示整個系統的運作方式。  
  
 您可利用系統監視器取得有關目前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 活動與效能的統計資料。 使用系統監視器可以：  
  
-   同時從任意多台電腦中檢視資料。  
  
-   檢視與變更圖表以反映目前的活動，並顯示計數器數值，其更新頻率是使用者自訂的。  
  
-   從圖表、記錄檔、警示記錄檔和報表中將資料匯出至試算表或資料庫應用程式內，以便作進一步的處理與列印。  
  
-   加入系統警示，將事件列在警示記錄檔，並且可以發出網路警示來通知您。  
  
-   當計數器數值首次或每次超過或低於某個使用者自訂的數值時，就執行預先定義的應用程式。  
  
-   建立記錄檔，裡面包含不同電腦之各種物件的相關資料。  
  
-   將其他現存記錄檔的資料附加到某個檔案的選取區段內，以構成長期的封存。  
  
-   檢視目前的活動報告，或使用現有的記錄檔來建立報告。  
  
-   儲存個別的圖表、警示、記錄檔、報告設定，或整個工作空間設定，以便重複使用。  
  
    > [!NOTE]  
    >  在 Windows NT 4.0 之後，「系統監視器」已取代「效能監視器」。 您可以使用系統監視器或效能監視器進行這些工作。  
  
## <a name="system-monitor-performance"></a>系統監視器效能  
 當您監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與 Microsoft Windows 作業系統，以研究效能相關的問題時，一開始可集中於三個主要領域上：  
  
-   磁碟活動  
  
-   處理器使用情形  
  
-   記憶體使用狀況  
  
 監視正在執行系統監視器的電腦，可能會稍微影響電腦的效能； 因此，您可將「系統監視器」資料記錄到另一個磁碟 (或電腦)，以減少對受監視電腦的影響，或從遠端電腦執行「系統監視器」。 請只監視有興趣的計數器。 如果您監視太多計數器，系統會將資源使用狀況負擔加入監視處理序，並且會影響正在監視的電腦之效能。  
  
## <a name="system-monitor-tasks"></a>系統監視器工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述使用系統監視器的時機，並討論使用系統監視器時的效能負擔。|[執行系統監視器](run-system-monitor.md)|  
|描述如何監視磁碟計數器以判定磁碟活動與其 SQL Server 元件所產生之 I/O 數量。|[監視磁碟使用量](monitor-disk-usage.md)|  
|描述如何監視 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，以判定 CPU 使用率是否在正常範圍內。|[監視 CPU 使用量](monitor-cpu-usage.md)|  
|描述如何監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，以確認記憶體使用量在正常範圍內。|[監視記憶體使用量](monitor-memory-usage.md)|  
|描述如何建立警示，讓它在達到系統監視器計數器的臨界值時引發。|[建立 SQL Server 資料庫警示](create-a-sql-server-database-alert.md)|  
|描述如何建立圖表、警示、記錄與報表，以監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。|[建立圖表、警示、記錄和報表](create-charts-alerts-logs-and-reports.md)|  
|列出系統監視器用以監視電腦中正在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之活動的物件與計數器。|[使用 SQL Server 物件](use-sql-server-objects.md)|  
|列出系統監視器用以監視記憶體中 OLTP 活動的物件與計數器。|[XTP&#40;記憶體內部 OLTP&#41;效能計數器](../../integration-services/performance/performance-counters.md)|  
  
  
