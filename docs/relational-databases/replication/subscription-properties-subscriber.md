---
title: "訂閱屬性 - 訂閱者 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newsubwizard.subproperties.subscriber.f1
helpviewer_keywords: Subscription Properties dialog box
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0983dafd2e95edbec342c7a885c1182f6dc053a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="subscription-properties---subscriber"></a>訂閱屬性 - 訂閱者
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] 訂閱者端的 [訂閱屬性] 對話方塊可讓您檢視和設定提取訂閱的屬性。  
  
 **[訂閱屬性]** 對話方塊中的每個屬性包含一個描述。 按一下某個屬性，即可查看其在對話方塊底部顯示的描述。 此主題提供數個屬性的其他資訊。 屬性會依下列類別目錄分組：  
  
-   套用至所有訂閱的屬性。  
  
-   套用至交易式訂閱的屬性。  
  
-   套用至合併訂閱的屬性。  
  
 如果選項顯示為唯讀，則只有在建立訂閱時才能設定。 如果想要設定新增訂閱精靈中無法使用的選項，請以預存程序建立訂閱。 如需相關資訊，請參閱 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md) 及 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)。  
  
> [!NOTE]  
>  如果尚未建立訂閱的散發代理程式或合併代理程式，則不會顯示許多訂閱屬性。 若要建立提取訂閱的代理程式作業，請執行 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md) (適用於快照式或交易式發行集訂閱) 或 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) (適用於合併式發行集訂閱)。  
  
## <a name="options-for-all-subscriptions"></a>所有訂閱的選項。  
 **初始化快照集的發行資料**  
 決定使用快照集 (預設值) 或透過另一種方法來初始化訂閱。 如需初始化訂閱的詳細資訊，請參閱[初始化訂閱](../../relational-databases/replication/initialize-a-subscription.md)。  
  
 **快照集位置**  
 決定初始化或重新初始化期間存取快照集檔案的位置。 此位置可以是下列其中一個值：  
  
-   **[預設位置]**：設定散發者時所定義的預設位置。 如需詳細資訊，請參閱[指定預設快照集位置 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)。  
  
-   **[替代資料夾]**：可在 **[發行集屬性]** 對話方塊中指定的替代位置。 如需相關資訊，請參閱 [Alternate Snapshot Folder Locations](../../relational-databases/replication/alternate-snapshot-folder-locations.md)。  
  
-   **[動態快照集資料夾]**：使用參數化資料列篩選器之合併式發行集的快照集位置。 如需相關資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)。  
  
-   **[FTP 資料夾]**：可讓檔案傳輸通訊協定 (FTP) 伺服器存取的資料夾。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
 **快照集資料夾**  
 如果您針對 **[快照集位置]** 選項選取 **[預設位置]** 以外的任何值，都必須指定快照集資料夾的路徑。  
  
 **使用 Windows Synchronization Manager**  
 決定是否可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager 來同步處理此訂閱。  
  
 **Security**  
 按一下 **[代理程式處理帳戶]** 資料列，然後按一下屬性按鈕 (**...**)，即可變更在訂閱者端執行散發代理程式或合併代理程式的帳戶。 與連接相關的安全性選項會視訂閱的類型而定：  
  
-   針對交易式發行集的訂閱：若要變更散發代理程式連接到散發者所使用的帳戶，請按一下 **[散發者連接]**，然後按一下屬性按鈕 (**...**)。  
  
-   針對立即更新交易式發行集的訂閱：除了上述的散發者連接之外，您可以變更用來從訂閱者傳播變更至發行者的方法：按一下 **[發行者連接]**，然後按一下屬性按鈕 (**...**)。  
  
-   針對合併式發行集的訂閱，請按一下 **[發行者連接]**，然後按一下屬性按鈕 (**...**)。  
  
 如需有關每個代理程式所需之權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
## <a name="options-for-transactional-subscriptions"></a>交易式訂閱的選項  
 **可更新的訂閱**  
 決定訂閱者變更是否會複寫回發行者。 可以使用佇列更新或立即更新來複寫變更。 **[訂閱者更新方法]** 選項會決定要使用的方法。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
## <a name="options-for-merge-subscriptions"></a>合併訂閱的選項  
 **資料分割定義 (HOST_NAME)**  
 針對使用參數化篩選的發行集，合併式複寫會在同步處理過程中評估兩個系統函數之一 (如果篩選參考兩個函數，則兩個都會評估)，以決定訂閱者應接收的資料： **SUSER_SNAME()** 或 **HOST_NAME()**。 依預設， **HOST_NAME()** 會傳回執行合併代理程式之電腦的名稱，但是您可以在新增訂閱精靈中覆寫這個值。 如需參數化篩選與覆寫 **HOST_NAME()**的詳細資訊，請參閱＜ [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
 **[訂閱類型]** 和 **[優先權]**  
 顯示訂閱是客訂閱或主訂閱 (建立了訂閱之後就無法再變更)。 主訂閱可以將資料重新發行至其他訂閱者，並且可以指派衝突解決的優先權。  
  
 如果您在新增訂閱精靈中選取伺服器的訂閱類型，就會為訂閱者指定在衝突解決過程中使用的優先權  
  
 **以互動方式解決衝突**  
 決定在合併同步處理過程中，是否使用互動解析程式使用者介面來解決衝突。 這需要 **[使用 Windows Synchronization Manager]** 的值為 **[啟用]**。 如需詳細資訊，請參閱 [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
 **Web 同步處理**  
 **[使用 Web 同步處理]** 決定是否連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 伺服器來同步處理訂閱。 只有啟用 Web 同步處理的發行集時，才能使用此選項。 如需詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。  
  
 如果針對 **[使用 Web 同步處理]** 選取 **[True]**：  
  
-   在 **[Web 伺服器位址]**中輸入 IIS 伺服器的完整位址。  
  
-   按一下 **[Web 伺服器連接]** 資料列，然後按一下屬性按鈕 (**...**)，即可設定或變更訂閱者連接到 IIS 伺服器的帳戶。  
  
-   必要時變更 **[Web 伺服器逾時]** 。 逾時是 Web 同步處理要求過期之前的時間長度 (以秒為單位)。  
  
 如需有關組態的詳細資訊，請參閱＜ [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [檢視及修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
