---
title: "處理複寫代理程式設定檔 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- agents [SQL Server replication], profiles
- profiles [SQL Server], replication agents
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: "49"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bb8f0adad4b35ec6fd2ca66bd6733d1cee92a65
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="work-with-replication-agent-profiles"></a>處理複寫代理程式設定檔
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中處理複寫代理程式設定檔。 每個複寫代理程式的行為由一組可在代理程式設定檔中設定的參數來控制。 各代理程式都有預設的設定檔，某些代理程式還擁有其他預先定義的設定檔；在某一給定時刻，代理程式只使用一個設定檔。  
  
 **本主題內容**  
  
-   **若要處理複寫代理程式設定檔，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   存取代理程式設定檔對話方塊  
  
    -   為代理程式指定設定檔  
  
    -   建立設定檔  
  
    -   修改設定檔  
  
    -   刪除設定檔  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   建立設定檔  
  
    -   修改設定檔  
  
    -   刪除設定檔  
  
    -   在同步處理期間使用代理程式設定檔  
  
    -   Transact-SQL 範例  
  
     [Replication Management Objects](#RMOProcedure)  
  
    -   建立設定檔  
  
    -   修改設定檔  
  
    -   刪除設定檔  
  
-   **後續操作：**[在變更代理程式參數之後](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> 若要透過 SQL Server Management Studio 存取代理程式設定檔對話方塊  
  
1.  在 [散發者屬性 - \<散發者>] 對話方塊的 [一般] 頁面上，按一下 [設定檔預設值]。  
  
#### <a name="to-access-the-agent-profiles-dialog-box-from-replication-monitor"></a>若要透過複寫監視器存取代理程式設定檔對話方塊  
  
-   若要開啟所有代理程式的對話方塊，請以滑鼠右鍵按一下「發行者」，然後按一下 **[代理程式設定檔]**。  
  
-   若要開啟單一代理程式的對話方塊：  
  
    1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
    2.  對於「散發代理程式」和「合併代理程式」設定檔，請以滑鼠右鍵按一下 **[所有訂閱]** 索引標籤上的訂閱，然後按一下 **[代理程式設定檔]**。 對於其他代理程式，請以滑鼠右鍵按一下 **[代理程式]** 索引標籤，然後按一下 **[代理程式設定檔]**。  
  
###  <a name="Specify_SSMS"></a> 若要為代理程式指定設定檔  
  
1.  如果 **[代理程式設定檔]** 對話方塊顯示一個以上的代理程式設定檔，請選取一個代理程式。  
  
2.  在 **[代理程式設定檔]** 方格的 **[新項目的預設值]** 資料行中選取一個設定檔。 依預設，設定檔只會套用至新發行集和訂閱的代理程式。  
  
3.  若要指定現有發行集或訂閱之選定類型的所有代理程式應使用此設定檔，請按一下 **[變更現有的代理程式]**。  
  
###  <a name="Modify_SSMS"></a> 若要檢視和編輯設定檔的相關參數  
  
1.  如果 **[代理程式設定檔]** 對話方塊顯示一個以上的代理程式設定檔，請選取一個代理程式。  
  
2.  按一下設定檔旁邊的屬性按鈕 (**...**)。  
  
3.  檢視 [\<設定檔名稱> 設定檔屬性] 對話方塊中的參數和值。  
  
    -   可以編輯使用者自訂之設定檔中的參數；但無法編輯預先定義之系統設定檔中的參數。  
  
    -   若要檢視代理程式的所有參數，請清除 **[只顯示這個設定檔中使用的參數]** 核取方塊。 如需有關代理程式參數的資訊，請參閱此主題結尾處的連結。  
  
4.  按一下 [ **關閉**]。  
  
###  <a name="Create_SSMS"></a> 若要建立使用者自訂的設定檔  
  
1.  如果 **[代理程式設定檔]** 對話方塊顯示一個以上的代理程式設定檔，請選取一個代理程式。  
  
2.  按一下 **[新增]**。  
  
3.  在 **[新增代理程式設定檔]** 初始化對話方塊中，選取新設定檔所依據的現有設定檔。  
  
4.  在 **[新增代理程式設定檔]** 對話方塊中，於 **[名稱]** 和 **[說明]** 文字方塊內輸入值。  
  
5.  修改參數以使其適用於設定檔。 若要檢視代理程式的所有參數，請清除 **[只顯示這個設定檔中使用的參數]** 核取方塊。 如需有關代理程式參數的資訊，請參閱此主題結尾處的連結。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> 若要刪除使用者自訂的設定檔  
  
1.  如果 **[代理程式設定檔]** 對話方塊顯示一個以上的代理程式設定檔，請選取一個代理程式。  
  
2.  如果設定檔與一個或多個代理程式相關聯，請變更這些代理程式的設定檔：  
  
    1.  請在 **[代理程式設定檔]** 方格中選取其他設定檔。  
  
    2.  按一下 **[變更現有的代理程式]**。  
  
        > [!NOTE]  
        >  這將變更現有發行集或訂閱之所有選定類型代理程式的設定檔，而不僅僅是使用您要刪除之設定檔的代理程式。  
  
3.  選取您要刪除的設定檔，然後按一下 **[刪除]**。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
###  <a name="Create_tsql"></a> 若要建立新的代理程式設定檔  
  
1.  在散發者端，執行 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)。 指定 **@name**、針對 **@profile_type** 指定 **@profile_type**的值，並針對 **@agent_type**指定下列其中一個值：  
  
    -   **@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     如果此設定檔將成為其複寫代理程式類型的新預設設定檔，請針對 **@profile_type** 指定 **@default**。 新設定檔的識別碼會使用 **@profile_id** 輸出參數傳回。 如此會根據給定的代理程式類型，建立具有一組設定檔參數的新設定檔。  
  
2.  在建立新設定檔之後，可以加入、移除或修改預設的參數來自訂該設定檔。  
  
###  <a name="Modify_tsql"></a> 若要修改現有的代理程式設定檔  
  
1.  在散發者端，執行 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 針對 **@agent_type**指定下列其中一個值：  
  
    -   **@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     這會傳回指定的代理程式類型的所有設定檔。 請注意結果集中要變更之設定檔的 **profile_id** 值。  
  
2.  在散發者端，執行 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)。 針對 **@profile_id**。 這會傳回設定檔的所有參數。 請注意要在設定檔中修改或移除的任何參數的名稱。  
  
3.  若要變更設定檔中的參數值，請執行 [sp_change_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)。 針對 **@profile_id**指定步驟 1 中的設定檔識別碼、針對 **@property**指定要變更的參數名稱，並針對 **@value**。  
  
    > [!NOTE]  
    >  您無法變更現有的代理程式設定檔，使其成為代理程式的預設設定檔， 而必須建立新的預設檔當做預設設定檔，如前述程序所示。  
  
4.  若要從設定檔移除參數，請執行 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)。 針對 **@profile_id** 指定步驟 1 中的設定檔識別碼，並針對 **@parameter_name**。  
  
5.  若要在設定檔中加入新參數，您必須執行下列動作：  
  
    -   查詢「散發者」端的 [MSagentparameterlist &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) 資料表，以判斷可針對每個代理程式類型所設定的設定檔參數。  
  
    -   在散發者端，執行 [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)。 針對 **@profile_id**指定步驟 1 中的設定檔識別碼、針對 **@parameter_name**指定要加入的有效參數的名稱，並針對 **@parameter_value**。  
  
###  <a name="Delete_tsql"></a> 若要刪除代理程式設定檔  
  
1.  在散發者端，執行 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 針對 **@agent_type**指定下列其中一個值：  
  
    -   **@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     這會傳回指定的代理程式類型的所有設定檔。 請注意結果集中要移除之設定檔的 **profile_id** 值。  
  
2.  在散發者端，執行 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)。 針對 **@profile_id**。  
  
###  <a name="Synch_tsql"></a> 若要在同步處理期間使用代理程式設定檔  
  
1.  在散發者端，執行 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 針對 **@agent_type**指定下列其中一個值：  
  
    -   **@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     這會傳回指定的代理程式類型的所有設定檔。 請注意結果集中要使用之設定檔的 **profile_name** 值。  
  
2.  如果代理程式是從代理程式作業啟動的，請編輯啟動代理程式的作業步驟，在 **-ProfileName** 命令列參數之後指定在步驟 1 中取得的 **profile_name** 值。 如需詳細資訊，請參閱[檢視並修改複寫代理程式命令提示字元參數 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)。  
  
3.  從命令提示字元啟動代理程式時，在 **-ProfileName** 命令列參數之後指定在步驟 1 中取得的 **profile_name** 值。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 此範例會針對名為 **custom_merge**的合併代理程式建立自訂的設定檔、變更 **-UploadReadChangesPerBatch** 參數的值、加入新的 **-ExchangeType** 參數，並傳回所建立之設定檔的相關資訊。  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 RMO  
  
###  <a name="Create_RMO"></a> 若要建立新的代理程式設定檔  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別的執行個體建立與「散發者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.AgentProfile> 類別的執行個體。  
  
3.  設定物件的下列屬性：  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> - 設定檔的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - <xref:Microsoft.SqlServer.Replication.AgentType> 值，指定為其建立設定檔的複寫代理程式類型。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - 在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
    -   (選擇性) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> - 設定檔的描述。  
  
    -   (選擇性) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> - 如果依預設這個 **T:Microsoft.SqlServer.Replication.AgentType** 的所有新代理程式作業都會使用這個設定檔，請將此屬性設定為 <xref:Microsoft.SqlServer.Replication.AgentType> 。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> 方法，以在伺服器上建立設定檔。  
  
5.  在伺服器上建立設定檔之後，就可以藉由加入、移除或變更複寫代理程式參數的值來加以自訂。  
  
6.  若要將設定檔指派給現有的複寫代理程式作業，請呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> 方法。 請針對 *distributionDBName* 傳遞散發資料庫的名稱，而針對 *agentID*傳遞作業識別碼。  
  
###  <a name="Modify_RMO"></a> 若要修改現有的代理程式設定檔  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別的執行個體建立與「散發者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別的執行個體。 傳遞在步驟 1 中建立的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 物件。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，請確認「散發者」存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> 方法。 傳遞 <xref:Microsoft.SqlServer.Replication.AgentType> 值，將傳回的設定檔縮減為特定的複寫代理程式類型。  
  
5.  從傳回的 <xref:Microsoft.SqlServer.Replication.AgentProfile> 取得想要的 <xref:System.Collections.ArrayList>物件，其中物件的 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 屬性符合設定檔的名稱。  
  
6.  呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile> 的下列其中一個方法來變更設定檔：  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> - 將支援的參數加入至設定檔，其中 *name* 是複寫代理程式參數的名稱， *value* 則是指定的值。 若要列舉給定代理程式類型的所有受支援的代理程式參數，請呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 物件的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> ，代表所有受支援的參數。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> - 從設定檔移除現有的參數，其中 *name* 是複寫代理程式參數的名稱。 若要列舉所有目前為設定檔所定義的代理程式參數，請呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 物件的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> ，代表此設定檔的現有參數。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> - 變更設定檔中現有參數的設定，其中 *name* 是代理程式參數的名稱，而 *newValue* 則是參數要變更成的值。 若要列舉所有目前為設定檔所定義的代理程式參數，請呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 物件的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> ，代表此設定檔的現有參數。 若要列舉所有受支援的代理程式參數設定，請呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 物件的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> ，代表所有受支援的參數值。  
  
###  <a name="Delete_RMO"></a> 若要刪除代理程式設定檔  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別的執行個體建立與「散發者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.AgentProfile> 類別的執行個體。 針對 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> ，設定步驟 1 的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>的設定檔名稱。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，則指定的名稱不正確，或伺服器上不存在該設定檔。  
  
4.  確認 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> 屬性是設定為 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>，這代表客戶的設定檔。 您不該移除 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> 的值為 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>的設定檔。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> 方法，從伺服器移除此物件代表的使用者自訂設定檔。  
  
##  <a name="FollowUp"></a> 後續操作：在變更代理程式參數之後  
 代理程式參數變更會在代理程式下次啟動時生效。 如果代理程式連續執行，則必須停止代理程式，然後重新啟動它。  
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  
