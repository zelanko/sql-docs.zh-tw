---
title: 發行集資訊、追蹤 Token (SQL Server 2005 和更新版本) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publicationinfo.tracertokens.f1
ms.assetid: a115ba95-17ae-45df-91bd-5a1a35f3745f
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: e4ec223179bf7fdb2e2fae250f95ab241ed1acf7
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770008"
---
# <a name="publication-information-tracer-tokens-sql-server-2005-and-later"></a>發行集資訊、追蹤 Token (SQL Server 2005 和更新版本)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[追蹤 Token]** 索引標籤，可讓您驗證連接並測量使用異動複寫之系統的延遲。 Token (即少量的資料) 會寫入發行集資料庫的交易記錄，會標示為典型的已複寫交易並且會透過系統傳送，它可允許計算：  
  
-   在發行者端認可交易和在散發者端之散發資料庫插入對應的命令之間，所經過的時間。  
  
-   在散發資料庫中插入命令和在訂閱者端認可對應的交易之間，所經過的時間。  
  
 根據以上計算，您可以回答許多問題，包括：  
  
-   哪些訂閱者在接收發行者的變更時，所花費的時間最長？  
  
-   預期會收到追蹤 Token 的訂閱者中，哪些沒有接收到 (如果有的話)？  
  
## <a name="options"></a>選項。  
 若要變更方格顯示資料的方式，請以滑鼠右鍵按一下方格，然後按一下下列其中一個選項：  
  
-   **排序**：在 [排序資料行]  對話方塊中排序一個或多個資料行。  
  
-   **選擇要顯示的資料行**：選取要顯示哪些資料行，以及這些資料行在 [選擇資料行]  對話方塊中的顯示順序。  
  
-   **篩選**：根據 [篩選設定]  對話方塊中的資料行值，篩選方格中的資料列。  
  
-   **清除篩選**：清除方格的所有篩選設定。  
  
 篩選設定是每個方格特有的設定。 資料行選取和排序會套用至所有相同類型的方格，例如每個發行者的發行集方格。  
  
 **插入追蹤**  
 按一下即可在發行者端的交易記錄中插入追蹤 Token。  
  
 **插入的時間**  
 選取插入追蹤 Token 的時間，來顯示該時間的延遲資訊。 依預設，會顯示最近時間的資訊。  
  
> [!NOTE]  
>  追蹤 Token 資訊與其他記錄資料的保留時間週期相同，這會由散發資料庫的記錄保留期限控制。 如需變更散發資料庫屬性的詳細資訊，請參閱[檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
 **訂閱**  
 發行集之每個訂閱的名稱。  
  
 **發行者到散發者**  
 在發行者端認可交易和在散發者端之散發資料庫插入對應的命令之間，所經過的時間。 值為 **[暫止]** 指出 Token 尚未到達散發者。 如果暫止狀態持續，請確定記錄讀取器代理程式在執行中。  
  
 **散發者到訂閱者**  
 在散發資料庫中插入命令和在訂閱者端認可對應的交易之間，所經過的時間。 值為 **[暫止]** 指出 Token 尚未到達訂閱者。 如果暫止狀態持續，請確定散發代理程式在執行中。  
  
 **延遲總計**  
 在發行者端認可交易和在訂閱者端認可對應的交易之間，所經過的時間。 這代表此時該訂閱者之複寫系統的端對端延遲。 值為 **[暫止]** 指出 Token 尚未到達訂閱者。  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止複寫代理程式 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [針對異動複寫測量延遲及驗證連線](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [使用複寫監視器監視效能](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)   
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
