---
title: "記憶體最佳化資料表的還原與復原 | Microsoft Docs"
ms.custom: 
ms.date: 12/31/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc4980acc94353003205668ef81653d6b9c55f75
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/19/2018
---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>記憶體最佳化資料表的還原與復原
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

復原或還原使用記憶體最佳化資料表之資料庫的基本機制，與僅使用磁碟資料表的資料庫機制類似。 但是與磁碟資料表不同之處在於，記憶體最佳化資料表必須載入記憶體中，資料庫才能供使用者存取。 這項需求會在資料庫復原中新增一個新步驟。  
  
如果伺服器的可用記憶體不足，則資料庫復原會失敗，並將資料庫標示為有疑問。 若要解決此問題，請參閱[解決記憶體不足問題](resolve-out-of-memory-issues.md)。 
  
## <a name="factors-that-affect-load-time"></a>影響載入時間的因素
在復原或還原作業期間，記憶體中 OLTP 引擎會讀取資料和差異檔案，以便將資料載入實體記憶體中。 載入時間是由以下條件所決定：  
  
-   要載入的資料數量。  
  
-   連續 I/O 頻寬。  
  
-   平行處理原則的程度，取決於檔案容器和處理器核心的數量。  
  
-   記錄檔記錄的數目，這些記錄位於需要重做之記錄檔的使用中部分。  

## <a name="phases-of-recovery"></a>修復階段
當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動時，每個資料庫都會經歷包括三個階段的復原階段：  
  
1.  **分析**。 在這個階段中，使用中交易記錄上會進行一個行程，用以偵測認可和未認可的交易。 記憶體中 OLTP 引擎會識別要載入的檢查點，並預先載入其系統資料表記錄項目。 另外還會處理一些檔案配置記錄檔記錄。  
  
2.  **取消復原**。 這個階段會在磁碟資料表和記憶體最佳化資料表上同時執行。  
  
    - 對於磁碟資料表，資料庫會移至目前的時間點，並取得未認可交易所採用的鎖定。  
  
    - 對於記憶體最佳化的資料表，來自資料和差異檔案組的資料會載入到記憶體。 然後會根據上一個持久性檢查點的作用中交易記錄檔更新資料。  
  
    前述在磁碟和記憶體最佳化資料表上的作業完成時，資料庫即可供存取。  
  
3.  **復原**。 在這個階段中，未認可的交易會回復。  
  
## <a name="process-for-improving-load-time"></a>改善載入時間的程序
將記憶體最佳化資料表載入記憶體中可能會影響復原時間目標 (RTO) 的效能。 為了改善從資料和差異檔案載入記憶體最佳化資料的時間，記憶體中 OLTP 引擎會平行載入資料/差異檔案，如下所示：  
  
-   **建立差異對應篩選**。 差異檔案會儲存已刪除資料列的參考。 每個容器會有一個執行緒讀取差異檔案，並建立差異對應篩選 (記憶體最佳化資料檔案群組可包含一或多個容器)。  
  
-   **將資料檔案作為資料流**。 建立差異對應篩選之後，就會使用與邏輯 CPU 數目相等的執行緒數目讀取資料檔案。 每個執行緒會讀取資料列、檢查相關聯的差異對應，並且只有在資料列未標示為已刪除時，才會將資料列插入至資料表。 在下圖中，復原的這個部分可能繫結於 CPU：  
  
    ![資料串流至經記憶體最佳化的資料表](../../relational-databases/in-memory-oltp/media/memory-optimized-tables.gif "資料串流至經記憶體最佳化的資料表")  
  
## <a name="specific-cases-of-slow-load-times"></a>緩慢載入時間的特定案例
經記憶體最佳化的資料表通常能夠以 I/O 速度載入記憶體中，但是將資料列載入到記憶體中的速度有時會變慢。 這些特定情況包括：  
  
-   雜湊索引的值區計數過低可能會導致過多衝突，造成插入資料列的速度變慢。 這種情況通常會導致整體 CPU 使用量變高，尤其是接近復原結束時。 如果您已正確設定雜湊索引，它應該不會影響復原時間。  
  
-   具有一或多個非叢集索引的大型記憶體最佳化資料表可能會造成高 CPU 使用率。 不同於在建立時調整值區計數大小的雜湊索引，非叢集索引會動態成長。  
  
## <a name="see-also"></a>另請參閱  
 [備份、還原及復原記憶體最佳化資料表](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
