---
title: 重新執行追蹤資料表 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 6a0ad817-3d8d-4495-889d-c66a7ef9e8bb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e80a18cef595ae3543aba8a656aca9267607e38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240485"
---
# <a name="replay-a-trace-table-sql-server-profiler"></a>重新執行追蹤資料表 (SQL Server Profiler)
  重新執行是開啟儲存的追蹤並重新執行該追蹤的能力。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 多執行緒播放引擎功能，可以模擬使用者連接及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 重新執行在排解應用程式或處理序的疑難問題時很有用。 您識別問題並實作更正時，針對更正的應用程式或處理序執行發現可能問題的追蹤。 然後，重新執行原始追蹤並比較結果。  
  
 除了您要監視的其他任何事件類別以外，還必須擷取特定的事件類別以便重新執行。 依預設，如果您使用 **TSQL_Replay** 追蹤範本，就會擷取這些事件。 如需詳細資訊，請參閱 [Replay Requirements](replay-requirements.md)。  
  
### <a name="to-replay-a-trace-table"></a>若要重新執行追蹤資料表  
  
1.  開啟內含重新執行時所需事件類別的追蹤資料表。  
  
2.  在 [重新執行]  功能表上按一下 [開始]  ，然後連接到您要重新執行追蹤的伺服器執行個體。  
  
3.  在 [重新執行組態]  對話方塊的 [基本重新執行選項]  索引標籤上，指定 [重新執行伺服器]  。 按一下 [變更]  ，以變更 [重新執行伺服器]  方塊中所顯示的伺服器。  
  
4.  選擇性，選取下列要儲存重新執行之目的地的其中之一：  
  
    -   [儲存至檔案]  ，指定用來儲存重新執行的檔案。  
  
    -   [儲存至資料表]  ，會指定要儲存重新執行的資料庫資料表。  
  
5.  選擇 [以追蹤事件的順序重新執行事件]  或 [使用多執行緒重新執行事件]  。 下列資料表說明這些設定之間的差異。  
  
    |選項|描述|  
    |------------|-----------------|  
    |**依照追蹤的順序重新執行事件**|以記錄事件的順序重新執行事件。 此選項會啟動偵錯。|  
    |**使用多執行緒重新執行事件**|這個選項使用多個執行緒重新執行每個事件，不受順序的限制。 這個選項會將效能最佳化。|  
  
6.  選取 [顯示重新執行結果]  ，在重新執行時檢視其過程。  
  
7.  或者按一下 [進階重新執行選項]  索引標籤，指定下列選項：  
  
    -   若要重新執行所有伺服器處理序識別碼 (SPID)，請選取 [重新執行系統 SPID]  。  
  
    -   若要限制只重新執行屬於特定 SPID 的處理序，請選取 [只重新執行一個 SPID]  。 在 [要重新執行的 SPID]  方塊中，輸入 SPID。  
  
    -   若要重新執行在特定時間週期內產生的事件，請選取 [依日期和時間限制重新執行]  。 選取 [開始時間]  與 [結束時間]  的日期和時間，指定重新執行中包含的時間週期。  
  
    -   若要控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在重新執行期間管理處理序的方式，請設定 [健全狀況監視器選項]  。  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL Server Profiler 所需的權限](sql-server-profiler.md)   
 [重新執行追蹤](replay-traces.md)   
 [開啟追蹤資料表 &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
