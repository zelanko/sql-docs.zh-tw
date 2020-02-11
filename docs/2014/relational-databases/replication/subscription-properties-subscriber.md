---
title: SQL Server 複寫訂閱屬性-訂閱者 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subproperties.subscriber.f1
- sql12.rep.newsubwizard.subproperties.publisher.f1
helpviewer_keywords:
- Subscription Properties dialog box
ms.assetid: bef66929-3234-4a45-8ec4-3b271519d07a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: af9cb7612837021b156fb8f467899f0e23ef1555
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250264"
---
# <a name="sql-server-replication-subscription-properties"></a>SQL Server 複寫訂用帳戶屬性 
本節提供有關 [**訂閱屬性**] 對話方塊的資訊。 

## <a name="publisher-properties"></a>發行者屬性 
  在發行者端的 **[訂閱屬性]** 對話方塊，可以讓您檢視和設定發送訂閱的屬性。 您也可以檢視提取訂閱的某些屬性，但在訂閱者端的 **[訂閱屬性]** 對話方塊，會顯示其他屬性並允許修改屬性。  
  
 **[訂閱屬性]** 對話方塊中的每個屬性包含一個描述。 按一下某個屬性，即可查看其在對話方塊底部顯示的描述。 此主題提供了關於一些屬性的其他資訊，其中大多數屬性僅會針對發行者端的發送訂閱顯示。 屬性會依下列類別目錄分組：  
  
-   套用至所有訂閱的屬性。    
-   套用至交易式訂閱的屬性。    
-   套用至合併訂閱的屬性。  
  
 如果選項顯示為唯讀，則只有在建立訂閱時才能設定。 如果想要設定新增訂閱精靈中無法使用的選項，請以預存程序建立訂閱。 如需相關資訊，請參閱 [Create a Pull Subscription](create-a-pull-subscription.md) 及 [Create a Push Subscription](create-a-push-subscription.md)。  

  
### <a name="options-for-all-subscriptions"></a>所有訂閱的選項。  
 **安全性**  
 按一下 **[代理程式處理帳戶]** 資料列，然後按一下屬性 (**...**) 按鈕，即可變更散發代理程式或合併代理程式在散發者端用以執行的帳戶。 若要變更散發代理程式或合併代理程式連接到訂閱者時所用的帳戶，請按一下 **[訂閱者連接]**，然後按一下屬性按鈕 (**...**)。  
  
 如需有關每個代理程式所需之權限的詳細資訊，請參閱＜ [Replication Agent Security Model](security/replication-agent-security-model.md)＞。  
  
### <a name="publisher-options-for-transactional-subscriptions"></a>交易式訂閱的發行者選項  
 **防止交易迴圈**  
 決定散發代理程式是否要將源自訂閱者端的交易，傳送回到訂閱者端。 此選項適用於雙向異動複寫。 如需詳細資訊，請參閱[雙向異動複寫](transactional/bidirectional-transactional-replication.md)。  
  
 **可更新的訂用帳戶**  
 決定訂閱者變更是否會複寫回發行者。 可以使用佇列更新或立即更新來複寫變更。 
  **[訂閱者更新方法]** 選項會決定要使用的方法。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
### <a name="options-for-merge-subscriptions"></a>合併訂閱的選項  
 **資料分割定義（HOST_NAME）**  
 針對使用參數化篩選的發行集，合併式複寫會在同步處理過程中評估兩個系統函數之一 (如果篩選參考兩個函數，則兩個都會評估)，以決定訂閱者應接收的資料： **SUSER_SNAME()** 或 **HOST_NAME()**。 依預設， **HOST_NAME()** 會傳回執行合併代理程式之電腦的名稱，但是您可以在新增訂閱精靈中覆寫這個值。 如需參數化篩選與覆寫 **HOST_NAME()** 的詳細資訊，請參閱＜ [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
 **訂**用帳戶類型和**優先順序**  
 顯示訂閱是客訂閱或主訂閱 (建立了訂閱之後就無法再變更)。 主訂閱可以將資料重新發行至其他訂閱者，並且可以指派衝突解決的優先權。  
  
 如果您在新增訂閱精靈中選取伺服器的訂閱類型，就會為訂閱者指定在衝突解決過程中使用的優先權。  
  
 **以互動方式解決衝突**  
 決定在合併同步處理過程中，是否使用互動解析程式使用者介面來解決衝突。 這需要 **[使用 Windows Synchronization Manager]** 的值為 **[啟用]**。 如需詳細資訊，請參閱 [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md)。  


## <a name="subscriber-properties"></a>訂閱者屬性
  訂閱者端的 [**訂閱屬性**] 對話方塊可讓您查看和設定提取訂閱的屬性。  
  
 
  **[訂閱屬性]** 對話方塊中的每個屬性包含一個描述。 按一下某個屬性，即可查看其在對話方塊底部顯示的描述。 此主題提供數個屬性的其他資訊。 屬性會依下列類別目錄分組：  
  
-   套用至所有訂閱的屬性。    
-   套用至交易式訂閱的屬性。   
-   套用至合併訂閱的屬性。  
  
 如果選項顯示為唯讀，則只有在建立訂閱時才能設定。 如果想要設定新增訂閱精靈中無法使用的選項，請以預存程序建立訂閱。 如需相關資訊，請參閱 [Create a Pull Subscription](create-a-pull-subscription.md) 及 [Create a Push Subscription](create-a-push-subscription.md)。  
  
> [!NOTE]  
>  如果尚未建立訂閱的散發代理程式或合併代理程式，則不會顯示許多訂閱屬性。 若要建立提取訂閱的代理程式作業，請執行 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) (適用於快照式或交易式發行集訂閱) 或 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql) (適用於合併式發行集訂閱)。  
  
### <a name="options-for-all-subscriptions"></a>所有訂閱的選項。  
 **從快照集初始化已發行的資料**  
 決定使用快照集 (預設值) 或透過另一種方法來初始化訂閱。 如需初始化訂閱的詳細資訊，請參閱[初始化訂閱](initialize-a-subscription.md)。  
  
 **快照集位置**  
 決定初始化或重新初始化期間存取快照集檔案的位置。 此位置可以是下列其中一個值：  
  
-   **預設位置**：設定散發者時所定義的預設位置。 如需詳細資訊，請參閱[指定預設快照集位置](snapshot-options.md#snapshot-folder-locations)。    
-   [**替代資料夾**]：可在 [**發行集屬性**] 對話方塊中指定的替代位置。 如需相關資訊，請參閱 [Alternate Snapshot Folder Locations](alternate-snapshot-folder-locations.md)。    
-   **動態快照集資料夾**：使用參數化資料列篩選器之合併式發行集的快照集位置。 如需詳細資訊，請參閱 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)。  
-   [ **Ftp 資料夾**]：檔案傳輸通訊協定（FTP）伺服器可存取的資料夾。 如需詳細資訊，請參閱[透過 FTP 傳送快照集](transfer-snapshots-through-ftp.md)。  
  
 **快照集資料夾**  
 如果您針對 **[快照集位置]** 選項選取 **[預設位置]** 以外的任何值，都必須指定快照集資料夾的路徑。  
  
 **使用 Windows 同步處理管理員**  
 決定是否可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Synchronization Manager 來同步處理此訂閱。  
  
 **安全性**  
 按一下 **[代理程式處理帳戶]** 資料列，然後按一下屬性按鈕 (**...**)，即可變更在訂閱者端執行散發代理程式或合併代理程式的帳戶。 與連接相關的安全性選項會視訂閱的類型而定：  
  
-   針對交易式發行集的訂閱：若要變更散發代理程式連接到散發者所使用的帳戶，請按一下 **[散發者連接]**，然後按一下屬性按鈕 (**...**)。    
-   針對立即更新交易式發行集的訂閱：除了上述的散發者連接之外，您可以變更用來從訂閱者傳播變更至發行者的方法：按一下 **[發行者連接]**，然後按一下屬性按鈕 (**...**)。  
-   針對合併式發行集的訂閱，請按一下 **[發行者連接]**，然後按一下屬性按鈕 (**...**)。  
  
 如需有關每個代理程式所需之權限的詳細資訊，請參閱＜ [Replication Agent Security Model](security/replication-agent-security-model.md)＞。  
  
### <a name="options-for-transactional-subscriptions"></a>交易式訂閱的選項  
 **可更新的訂用帳戶**  
 決定訂閱者變更是否會複寫回發行者。 可以使用佇列更新或立即更新來複寫變更。 
  **[訂閱者更新方法]** 選項會決定要使用的方法。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
### <a name="options-for-merge-subscriptions"></a>合併訂閱的選項  
 **資料分割定義（HOST_NAME）**  
 針對使用參數化篩選的發行集，合併式複寫會在同步處理過程中評估兩個系統函數之一 (如果篩選參考兩個函數，則兩個都會評估)，以決定訂閱者應接收的資料： **SUSER_SNAME()** 或 **HOST_NAME()**。 依預設， **HOST_NAME()** 會傳回執行合併代理程式之電腦的名稱，但是您可以在新增訂閱精靈中覆寫這個值。 如需參數化篩選與覆寫 **HOST_NAME()** 的詳細資訊，請參閱＜ [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
 **訂**用帳戶類型和**優先順序**  
 顯示訂閱是客訂閱或主訂閱 (建立了訂閱之後就無法再變更)。 主訂閱可以將資料重新發行至其他訂閱者，並且可以指派衝突解決的優先權。  
  
 如果您在新增訂閱精靈中選取伺服器的訂閱類型，就會為訂閱者指定在衝突解決過程中使用的優先權  
  
 **以互動方式解決衝突**  
 決定在合併同步處理過程中，是否使用互動解析程式使用者介面來解決衝突。 這需要 **[使用 Windows Synchronization Manager]** 的值為 **[啟用]**。 如需詳細資訊，請參閱 [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md)。  
  
 **Web 同步處理**  
 [**使用 Web 同步**處理] 決定是否連接[!INCLUDE[msCoName](../../includes/msconame-md.md)]到 Internet Information Services （IIS）伺服器來同步處理訂閱。 只有啟用 Web 同步處理的發行集時，才能使用此選項。 如需詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)＞。  
  
 如果針對 **[使用 Web 同步處理]** 選取 **[True]**：  
  
-   在 **[Web 伺服器位址]** 中輸入 IIS 伺服器的完整位址。   
-   按一下 **[Web 伺服器連接]** 資料列，然後按一下屬性按鈕 (**...**)，即可設定或變更訂閱者連接到 IIS 伺服器的帳戶。   
-   必要時變更 **[Web 伺服器逾時]** 。 逾時是 Web 同步處理要求過期之前的時間長度 (以秒為單位)。  
  
 如需有關組態的詳細資訊，請參閱＜ [Configure Web Synchronization](configure-web-synchronization.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [查看和修改提取訂閱屬性](view-and-modify-pull-subscription-properties.md)   
 [檢視及修改發送訂閱屬性](view-and-modify-push-subscription-properties.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
