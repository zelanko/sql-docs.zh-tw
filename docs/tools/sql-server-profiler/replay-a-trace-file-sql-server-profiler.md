---
title: 重新執行追蹤檔案 (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 9e361275-c8fd-4499-8389-242cf8e27415
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fe3a0971be4494c62d7e29a9641ed82655126a23
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031457"
---
# <a name="replay-a-trace-file-sql-server-profiler"></a>重新執行追蹤檔案 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  重新執行是開啟儲存的追蹤並重新執行該追蹤的能力。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 多執行緒播放引擎功能，可以模擬使用者連接及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證。 重新執行在排解應用程式或處理序的疑難問題時很有用。 您識別問題並實作更正時，針對更正的應用程式或處理序執行發現可能問題的追蹤。 然後，重新執行原始追蹤並比較結果。  
  
 除了您要監視的其他任何事件類別以外，還必須擷取特定的事件類別以便重新執行。 依預設，如果您使用 **TSQL_Replay** 追蹤範本，就會擷取這些事件。 如需詳細資訊，請參閱 [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md)。  
  
### <a name="to-replay-a-trace-file"></a>若要重新執行追蹤檔案  
  
1.  在 [檔案]  功能表上，指向 [開啟]  ，然後按一下 [追蹤檔案]  。 選取追蹤檔案，其中包含重新執行所需的事件類別。  
  
2.  在 [重新執行]  功能表上按一下 [開始]  ，然後連接到您要重新執行追蹤的伺服器執行個體。  
  
3.  在 [重新執行組態]  對話方塊的 [基本重新執行選項]  索引標籤上，指定 [重新執行伺服器]  。 按一下 [變更]  ，變更 [重新執行伺服器]  方塊上所顯示的伺服器。  
  
4.  選擇性，選取下列要儲存重新執行之目的地的其中之一：  
  
    -   [儲存至檔案]  ，指定用來儲存重新執行的檔案。  
  
    -   [儲存至資料表]  ，指定用來儲存重新執行的資料庫資料表。  
  
5.  選擇 [以追蹤事件的順序重新執行事件]  或 [使用多執行緒重新執行事件]  。 下列資料表說明這些設定之間的差異。  
  
    |選項|Description|  
    |------------|-----------------|  
    |**依照追蹤的順序重新執行事件**|以記錄事件的順序重新執行事件。 此選項會啟動偵錯。|  
    |**使用多執行緒重新執行事件**|這個選項使用多個執行緒重新執行每個事件，不受順序的限制。 這個選項會將效能最佳化。|  
  
6.  選取 [顯示重新執行結果]  ，在重新執行時檢視其過程。  
  
7.  (選擇性) 按一下 [進階重新執行選項]  索引標籤，設定下列選項：  
  
    -   若要重新執行所有伺服器處理序識別碼 (SPID)，請選取 [重新執行系統 SPID]  。  
  
    -   若要限制只重新執行屬於特定 SPID 的處理序，請選取 [只重新執行一個 SPID]  。 在 [要重新執行的 SPID]  方塊中，輸入 SPID。  
  
    -   若要重新執行特定時間週期發生的事件，請選取 [依日期與時間限制重新執行]  。 選取 [開始時間]  與 [結束時間]  的日期和時間，指定重新執行中包含的時間週期。  
  
    -   若要控制 SQL Server 在重新執行期間管理處理序的方式，請設定 [健全狀況監視器選項]  。  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL Server Profiler 所需的權限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [重新執行追蹤](../../tools/sql-server-profiler/replay-traces.md)   
 [開啟追蹤檔案 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
