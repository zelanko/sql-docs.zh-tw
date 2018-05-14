---
title: 效能的監視與微調 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 16d40afb894e02b747870baef853196cfacecf5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-and-tune-for-performance"></a>效能的監視與微調
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  監視資料庫的目標在於評估伺服器的執行效能。 有效的監視包括定期建立目前效能的快照集以隔離造成問題的處理序，以及持續蒐集資料來追蹤效能趨勢。  
  
 持續進行的資料庫效能評估可協助您將回應時間降到最低並產生最大產能，以達最佳效能。 有效率的網路流量、磁碟 I/O 與 CPU 使用量是達到最佳效能的關鍵。 您必須徹底分析應用程式需求、了解資料的邏輯與實體結構、評估資料庫使用，以及商議使用衝突的折衷方案，如線上交易處理 (Online Transaction Processing，OLTP) 之於決策支援。  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>監視和微調資料庫效能  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Microsoft Windows 作業系統提供公用程式，以檢視資料庫的目前狀況並隨著狀況變更來追蹤效能。 您可以使用各種工具和技術來監視 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可協助您：  
  
-   判斷是否可以改善效能。 例如，監視常用查詢的回應時間，您可以判斷是否需要變更資料表的查詢或索引。  
  
-   評估使用者活動。 例如，藉由監視嘗試連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的使用者，您可以判斷安全性是否設定適當，並測試應用程式和開發系統。 例如，藉由監視執行中的 SQL 查詢，您可以判斷查詢是否撰寫正確並產生預期的結果。  
  
-   對問題進行疑難排解或對應用程式元件進行偵錯，例如預存程序。  
  
## <a name="monitoring-in-a-dynamic-environment"></a>動態環境中的監視  
變更條件會導致效能變更。 評估過程中，當使用者數目增加、使用者存取與連接方式變更、資料庫內容成長、用戶端應用程式變更、應用程式中的資料變更、查詢變得更複雜，以及網路流量提高時，效能也會跟著變更。 藉由使用工具來監視效能，可協助您找出條件變更或複雜查詢與效能變更之間的關聯。 **範例**：  
  
-   藉由監視常用查詢的回應時間，您可以判斷是否需要變更執行查詢之資料表的查詢或索引。  
  
-   藉由監視執行中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，您可以判斷查詢是否撰寫正確並產生預期的結果。  
  
-   藉由監視嘗試連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的使用者，您可以判斷安全性是否適當地設定，並對應用程式或開發系統進行測試。  
  
 回應時間就是將結果集的第一個資料列傳回給使用者所需的時間長度，以視覺化確認的形式表示查詢已經過處理了。 輸送量是指在指定的期間內，伺服器所處理的查詢總數。  
  
 隨著使用者數目的增加，伺服器資源的爭奪現象也會隨之增加，連帶使回應時間增加，整體輸送量降低。  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>監視和效能微調工作  
  
|主題| 工作|  
|-----------|----------------------|  
|[監視 SQL Server 元件](../../relational-databases/performance/monitor-sql-server-components.md)|監視任何 SQL Server 元件的必要步驟。|  
|[效能監視及微調工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|列出 SQL Server 可用的監視和微調工具。|  
|[建立效能基準](../../relational-databases/performance/establish-a-performance-baseline.md)|如何建立效能基準。|  
|[隔離效能問題](../../relational-databases/performance/isolate-performance-problems.md)|隔離資料庫效能問題。|  
|[找出瓶頸](../../relational-databases/performance/identify-bottlenecks.md)|監視和追蹤伺服器效能，以找出瓶頸。|  
|[伺服器效能與活動監視](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以及 Windows 效能和活動監視工具。|  
|[顯示並儲存執行計畫](../../relational-databases/performance/display-and-save-execution-plans.md)|顯示執行計畫，並將執行計畫儲存至 XML 格式的檔案。|  
|[即時查詢統計資料](../../relational-databases/performance/live-query-statistics.md)|顯示有關查詢執行步驟的即時統計資料。|  
|[使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|使用查詢存放區來自動擷取查詢、計劃和執行階段統計資料的記錄，並加以保留供您檢閱。|  
|[使用含有記憶體內部 OLTP 的查詢存放區](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)|記憶體最佳化資料表的考量。|  
|[使用查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)|使用查詢存放區的建議。|  
  
## <a name="see-also"></a>另請參閱  
 [將整個企業的管理自動化](http://msdn.microsoft.com/library/44d8365b-42bd-4955-b5b2-74a8a9f4a75f)   
 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)   
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
