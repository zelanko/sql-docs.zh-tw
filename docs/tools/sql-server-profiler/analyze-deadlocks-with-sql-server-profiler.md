---
title: "使用 SQL Server Profiler 分析死結 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process nodes [SQL Server Profiler]
- Profiler [SQL Server Profiler], deadlocks
- deadlocks [SQL Server], identifying cause
- resource nodes [SQL Server Profiler]
- graphs [SQL Server Profiler]
- SQL Server Profiler, deadlocks
- events [SQL Server], deadlocks
- edges [SQL Server Profiler]
ms.assetid: 72d6718f-501b-4ea6-b344-c0e653f19561
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 929b037e2d3bc844e284adb51e96f0e4c5b4e1f7
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="analyze-deadlocks-with-sql-server-profiler"></a>使用 SQL Server Profiler 分析死結
  使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 可識別死結的原因。 SQL Server 中有兩個或兩個以上的執行緒 (或處理序)，因為某些資源集而產生循環相依性時，就會發生死結。 利用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，您可以建立一個用來記錄、重新執行和顯示死結事件的追蹤，以便進行分析。  
  
 若要追蹤死結事件，請將 **Deadlock graph** 事件類別加入追蹤。 此事件類別會用死結相關處理序和物件的 XML 資料來擴展追蹤中的 **TextData** 資料行。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 可將 XML 文件擷取至死結 XML (.xdl) 檔案，您稍後可在 SQL Server Management Studio 中檢視該檔案。 您可以設定 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ，將 **Deadlock graph** 事件擷取到單一檔案 (其中包含所有的 **Deadlock graph** 事件)，或將各個事件擷取到不同的檔案。 這種擷取可以利用下列任一方法來完成：  
  
-   在追蹤組態時，使用 [事件擷取設定] 索引標籤。 請注意，您需在 [事件選取範圍] 索引標籤上選取 **Deadlock graph** 事件，這個索引標籤才會出現。  
  
-   使用 [檔案] 功能表上的 [擷取 SQL Server 事件] 選項。  
  
-   您也可以用滑鼠右鍵按一下特定事件，然後選擇 [擷取事件資料]，以擷取並儲存個別事件。  
  
## <a name="deadlock-graphs"></a>死結圖形  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 使用死結等待圖形 (deadlock wait-for graph) 來描述死結。 死結等待圖形包含處理序節點、資源節點，以及代表處理序與資源之間關聯性的邊緣。 等待圖形的元件定義如下表所示：  
  
 處理序節點  
 執行工作的執行緒；例如，INSERT、UPDATE 或 DELETE。  
  
 資源節點  
 資料庫物件；例如，資料表、索引或資料列。  
  
 邊緣  
 處理序與資源之間的關聯性。 當處理序等待資源時，會發生 **request** 邊緣； 當資源等待處理序時，則會發生 **owner** 邊緣。 邊緣描述中也會納入鎖定模式， 例如 [模式: X]。  
  
## <a name="deadlock-process-node"></a>死結處理序節點  
 在等待圖形中，處理序節點包含處理序的相關資訊。 下表說明處理序的元件。  
  
|元件|定義|  
|---------------|----------------|  
|伺服器處理序識別碼|伺服器處理序識別碼 (SPID)，伺服器指派給擁有鎖定之處理序的識別碼。|  
|伺服器批次識別碼|伺服器批次識別碼 (SBID)。|  
|執行內容識別碼|執行內容識別碼 (ECID)。 給定執行緒並和特定 SPID 關聯的執行內容識別碼。<br /><br /> ECID = {0, 1, 2, 3, ... *n*}，其中 0 一律代表主要或父執行緒，{1, 2, 3, ... *n*} 代表子執行緒。|  
|死結優先權|處理序的死結優先權。 如需可能值的詳細資訊，請參閱 [SET DEADLOCK_PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/set-deadlock-priority-transact-sql.md)。|  
|使用的記錄|處理序已使用的記錄檔空間量。|  
|擁有者識別碼|正在使用交易且目前正在等待鎖定之處理序的交易識別碼。|  
|交易描述項|說明交易狀態之交易描述項的指標。|  
|輸入緩衝區|目前處理序的輸入緩衝區，定義事件類型和正在執行的陳述式。 可能的值包括：<br /><br /> **語言**<br /><br /> **RPC**<br /><br /> **無**|  
|Statement|陳述式的類型。 可能的值為：<br /><br /> **NOP**<br /><br /> **SELECT**<br /><br /> **UPDATE**<br /><br /> **INSERT**<br /><br /> **DELETE**<br /><br /> **Unknown**|  
  
## <a name="deadlock-resource-node"></a>死結資源節點  
 在死結中，有兩個處理序正在互相等待彼此所保留的資源。 在死結圖形中，資源會顯示為資源節點。  
  
  
