---
title: 重新執行選項 (SQL Server Profiler) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
- health monitor [SQL Server]
- Replay Configuration dialog box
ms.assetid: 58761a25-a84f-4a90-9c61-97700bc5ad9c
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ffceaa31c30aec5a0d0911017a45fde592c427c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034956"
---
# <a name="replay-options-sql-server-profiler"></a>重新執行選項 (SQL Server Profiler)
  使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來重新執行擷取的追蹤之前，請在 [重新執行組態] 對話方塊中指定重新執行選項。 若要啟動此對話方塊，請開啟 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 中的重新執行追蹤檔案或資料表，然後在 [重新執行] 功能表上按一下 [啟動]。 如需有關重做追蹤時所需之權限的詳細資訊，請參閱＜ [Permissions Required to Run SQL Server Profiler](sql-server-profiler.md)＞。  
  
 本主題描述使用 [重新執行組態] 對話方塊所指定的選項。  
  
> [!NOTE]  
>  我們建議您使用分散式重新執行公用程式來重新執行密集的 OLTP 應用程式 (具有許多使用中並行連接或高輸送量)。 分散式重新執行公用程式可以從多部電腦重新執行追蹤資料，並有效模擬關鍵任務的工作負載。 如需詳細資訊，請參閱 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)。  
  
## <a name="basic-replay-options"></a>基本重新執行選項  
 **重新執行伺服器**  
 該伺服器是您要對其重新執行追蹤的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。 伺服器必須遵守 [重新執行需求](replay-requirements.md)中所描述的重新執行需求。  
  
 **儲存至檔案**  
 將重新執行追蹤的結果寫入輸出檔中，以供稍後檢視。 根據預設， [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 只會在螢幕上顯示重新執行追蹤的結果。  
  
 **儲存至資料表**  
 將重新執行追蹤的結果寫入資料庫資料表中，以供稍後檢視。  
  
 **重新執行執行緒的數目**  
 指定要同時使用的重新執行執行緒的數目。 數量愈大，在重新執行期間所耗用的資源就愈多，但重新執行的速度也愈快。 使用多執行緒時，就不會完整地維護事件順序。  
  
 **依照追蹤的順序重新執行事件**  
 可讓您使用偵錯方法，例如逐步執行每項追蹤。 如果沒有選取此選項，則重新執行作業不保證會以原先擷取事件的順序來重新執行事件。  
  
 **使用多執行緒重新執行事件**  
 最佳化效能，並停用偵錯。 它會依照針對特定伺服器處理序識別碼 (SPID) 記錄的順序來重新執行事件，但不保證 SPID 的順序。  
  
 **顯示重新執行結果**  
 顯示重新執行的結果。 這是預設選項。 若您重新執行的追蹤很大，您可能想要停用此選項來儲存磁碟空間。  
  
> [!NOTE]  
>  為得到最佳的重新執行效能，建議您選擇使用多執行緒來重新執行事件，並且不要選擇顯示重新執行的結果。  
  
## <a name="advanced-replay-options"></a>進階重新執行選項  
 **重新執行系統 SPID**  
 重新執行所有 SPID。 這是預設選項。  
  
 **只重新執行一個 SPID**  
 重新執行您從清單中選擇的 SPID 號碼。  
  
 **依日期和時間限制重新執行**  
 針對所指定的 [開始時間] 及 [結束時間] 來重新執行追蹤。  
  
 **健全狀況監視器等候間隔**  
 設定可允許處理序執行的時間量，時間一到，健全狀況監視器就會將其終止。  
  
 **健全狀況監視器輪詢間隔**  
 設定健全狀況監視器輪詢適用項目來加以終止的頻率。  
  
 **啟用 SQL Server 封鎖處理序監視器**  
 設定已封鎖之處理序監視器搜尋已封鎖或封鎖中處理序的頻率。  
  
## <a name="about-the-health-monitor"></a>關於健全狀況監視器  
 健全狀況監視器是一個應用程式執行緒，可監視有關重新執行追蹤的模擬處理序，並結束重新執行作業中被封鎖的處理序。 您可以在 [重新執行組態] 對話方塊的 [進階重新執行選項] 索引標籤中，指定健全狀況監視器要等候幾秒，再結束被封鎖的處理序 ([健全狀況監視器等候間隔])。 如果您將此間隔設為 0，則健全狀況監視器就永遠都不會結束重新執行追蹤中的模擬封鎖處理序。  
  
## <a name="see-also"></a>另請參閱  
 [重新執行追蹤](replay-traces.md)   
 [重新執行需求](replay-requirements.md)   
 [重新執行追蹤的考量&#40;SQL Server Profiler&#41;](considerations-for-replaying-traces-sql-server-profiler.md)  
  
  