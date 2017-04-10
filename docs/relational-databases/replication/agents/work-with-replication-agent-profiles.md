---
title: "處理複寫代理程式設定檔 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replication [SQL Server], agents and profiles"
  - "replication agent profiles [SQL Server]"
  - "agents [SQL Server replication], profiles"
  - "設定檔 [SQL Server], 複寫代理程式"
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
caps.latest.revision: 49
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 49
---
# 處理複寫代理程式設定檔
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中處理複寫代理程式設定檔。 每個複寫代理程式的行為由一組可在代理程式設定檔中設定的參數來控制。 各代理程式都有預設的設定檔，某些代理程式還擁有其他預先定義的設定檔；在某一給定時刻，代理程式只使用一個設定檔。  
  
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
  
-   **待處理︰**  [之後變更代理程式參數](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
###  <a name="Access_SSMS"></a> 若要透過 SQL Server Management Studio 存取代理程式設定檔對話方塊  
  
1.  在 **一般** 頁面 **散發者屬性-\< 散發者>** 對話方塊中，按一下 [ **設定檔預設**。  
  
#### 若要透過複寫監視器存取代理程式設定檔對話方塊  
  
-   若要開啟所有代理程式] 對話方塊中，「 發行者 」，以滑鼠右鍵按一下，然後按一下 [ **代理程式設定檔**。  
  
-   若要開啟單一代理程式的對話方塊：  
  
    1.  在複寫監視器的左窗格中展開發行者群組，展開發行者，然後按一下發行集。  
  
    2.  散發代理程式 」 和 「 合併代理程式設定檔，以滑鼠右鍵按一下訂閱 **所有訂閱** 索引標籤，然後再按一下 **代理程式設定檔**。 對於其他代理程式，以滑鼠右鍵按一下代理程式上 **代理程式** 索引標籤，然後再按一下 **代理程式設定檔**。  
  
###  <a name="Specify_SSMS"></a> 若要為代理程式指定設定檔  
  
1.  如果 **[代理程式設定檔]** 對話方塊顯示一個以上的代理程式設定檔，請選取一個代理程式。  
  
2.  在 **[代理程式設定檔]** 方格的 **[新項目的預設值]** 資料行中選取一個設定檔。 依預設，設定檔只會套用至新發行集和訂閱的代理程式。  
  
3.  若要指定現有發行集或訂閱之選定類型的所有代理程式應使用此設定檔，請按一下 **[變更現有的代理程式]**。  
  
###  <a name="Modify_SSMS"></a> 若要檢視和編輯設定檔的相關參數  
  
1.  如果 **[代理程式設定檔]** 對話方塊顯示一個以上的代理程式設定檔，請選取一個代理程式。  
  
2.  按一下屬性按鈕 (**...**) 設定檔旁邊。  
  
3.  檢視的參數和值在 **\< ProfileName> 設定檔屬性** 對話方塊。  
  
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
  
1.  在散發者 」 執行 [sp_add_agent_profile & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)。 指定 **@name**, ，值為 **1** 的 **@profile_type**, ，和下列其中一個值 **@agent_type**:  
  
    -   **1** - [複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [複寫記錄讀取器代理程式](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [複寫佇列讀取器代理程式](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     如果此設定檔將成為其複寫代理程式類型的新預設設定檔，請針對 **@default** 指定 **1**的值。 新的設定檔的識別碼會使用傳回 **@profile_id** 輸出參數。 如此會根據給定的代理程式類型，建立具有一組設定檔參數的新設定檔。  
  
2.  在建立新設定檔之後，可以加入、移除或修改預設的參數來自訂該設定檔。  
  
###  <a name="Modify_tsql"></a> 若要修改現有的代理程式設定檔  
  
1.  在散發者 」 執行 [sp_help_agent_profile & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 指定下列值的其中一個 **@agent_type**:  
  
    -   **1** - [複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [複寫記錄讀取器代理程式](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [複寫佇列讀取器代理程式](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     這會傳回指定的代理程式類型的所有設定檔。 記下的值 **profile_id** 結果集中要變更之設定檔。  
  
2.  在散發者 」 執行 [sp_help_agent_parameter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)。 指定步驟 1 中的設定檔識別碼 **@profile_id**。 這會傳回設定檔的所有參數。 請注意要在設定檔中修改或移除的任何參數的名稱。  
  
3.  若要變更設定檔中的參數值，請執行 [sp_change_agent_profile & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-change-agent-profile-transact-sql.md)。 指定步驟 1 中的設定檔識別碼 **@profile_id**, ，若要變更參數名稱 **@property**, ，和新值之參數的 **@value**。  
  
    > [!NOTE]  
    >  您無法變更現有的代理程式設定檔，使其成為代理程式的預設設定檔， 而必須建立新的預設檔當做預設設定檔，如前述程序所示。  
  
4.  若要從設定檔移除參數，執行 [sp_drop_agent_parameter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)。 指定步驟 1 中的設定檔識別碼 **@profile_id** 和要移除的參數名稱 **@parameter_name**。  
  
5.  若要在設定檔中加入新參數，您必須執行下列動作：  
  
    -   查詢 [MSagentparameterlist & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) 判斷哪一個設定檔參數可以為每個代理程式類型的散發者端的資料表。  
  
    -   在散發者 」 執行 [sp_add_agent_parameter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)。 指定步驟 1 中的設定檔識別碼 **@profile_id**, ，若要加入的有效參數名稱 **@parameter_name**, ，並為參數的值 **@parameter_value**。  
  
###  <a name="Delete_tsql"></a> 若要刪除代理程式設定檔  
  
1.  在散發者 」 執行 [sp_help_agent_profile & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 指定下列值的其中一個 **@agent_type**:  
  
    -   **1** - [複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [複寫記錄讀取器代理程式](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [複寫佇列讀取器代理程式](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     這會傳回指定的代理程式類型的所有設定檔。 記下的值 **profile_id** 結果集中要移除之設定檔。  
  
2.  在散發者 」 執行 [sp_drop_agent_profile & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)。 指定步驟 1 中的設定檔識別碼 **@profile_id**。  
  
###  <a name="Synch_tsql"></a> 若要在同步處理期間使用代理程式設定檔  
  
1.  在散發者 」 執行 [sp_help_agent_profile & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)。 指定下列值的其中一個 **@agent_type**:  
  
    -   **1** - [複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [複寫記錄讀取器代理程式](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [複寫佇列讀取器代理程式](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     這會傳回指定的代理程式類型的所有設定檔。 記下的值 **profile_name** 結果集中使用的設定檔。  
  
2.  如果代理程式已啟動代理程式作業中，編輯啟動代理程式，以指定的值的作業步驟 **profile_name** 之後的步驟 1 中取得 **-ProfileName** 命令列參數。 如需詳細資訊，請參閱 [檢視和修改複寫代理程式命令提示字元參數 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)。  
  
3.  從命令提示字元啟動代理程式，當指定的值 **profile_name** 之後的步驟 1 中取得 **-ProfileName** 命令列參數。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 這個範例會建立名為 「 合併代理程式的自訂設定檔 **custom_merge**, ，變更的值 **-UploadReadChangesPerBatch** 參數，將新 **-ExchangeType** 參數和傳回有關所建立的設定檔。  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> 使用 RMO  
  
###  <a name="Create_RMO"></a> 若要建立新的代理程式設定檔  
  
1.  建立連接到散發者 」 使用的執行個體 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.AgentProfile> 類別。  
  
3.  設定物件的下列屬性：  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> -設定檔的名稱。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - <xref:Microsoft.SqlServer.Replication.AgentType> 值，指定複寫代理程式正在建立設定檔的類型。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立。  
  
    -   （選擇性） <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> -設定檔的描述。  
  
    -   （選擇性） <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> -將此屬性設定為 **true** 如果所有的新代理程式作業，這個 <xref:Microsoft.SqlServer.Replication.AgentType> 預設會使用此設定檔。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> 方法，以在伺服器上建立設定檔。  
  
5.  在伺服器上建立設定檔之後，就可以藉由加入、移除或變更複寫代理程式參數的值來加以自訂。  
  
6.  若要將設定檔指派給現有的複寫代理程式作業，呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> 方法。 請針對 *distributionDBName* 傳遞散發資料庫的名稱，而針對 *agentID*傳遞作業識別碼。  
  
###  <a name="Modify_RMO"></a> 若要修改現有的代理程式設定檔  
  
1.  建立連接到散發者 」 使用的執行個體 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別。 傳遞 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中建立的物件。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，請確認「散發者」存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> 方法。 傳遞 <xref:Microsoft.SqlServer.Replication.AgentType> 縮小傳回的特定類型的複寫代理程式設定檔的值。  
  
5.  取得想要 <xref:Microsoft.SqlServer.Replication.AgentProfile> 從傳回的物件 <xref:System.Collections.ArrayList>, ，其中 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 之物件的屬性會比對設定檔名稱。  
  
6.  呼叫下列方法的其中一個 <xref:Microsoft.SqlServer.Replication.AgentProfile> 變更的設定檔︰  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> -將支援的參數加入至設定檔，其中 *名稱* 是複寫代理程式參數的名稱和 *值* 是指定的值。 若要列舉給定代理程式類型的所有支援的代理程式參數，呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 物件，表示所有支援的參數。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> -從設定檔，移除現有的參數位置 *名稱* 是複寫代理程式參數的名稱。 若要列舉目前設定檔定義的所有代理程式參數，呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 代表現有的參數，此設定檔的物件。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> -變更現有參數在設定檔，設定其中 *名稱* 是代理程式參數的名稱和 *newValue* 是所要變更參數的值。 若要列舉目前設定檔定義的所有代理程式參數，呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> 代表現有的參數，此設定檔的物件。 若要列舉所有支援的代理程式參數設定，請呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> 方法。 這個方法會傳回 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> 代表支援的所有參數值的物件。  
  
###  <a name="Delete_RMO"></a> 若要刪除代理程式設定檔  
  
1.  建立連接到散發者 」 使用的執行個體 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.AgentProfile> 類別。 設定的設定檔名稱 <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法傳回 **false**，則指定的名稱不正確，或伺服器上不存在該設定檔。  
  
4.  確認 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> 屬性設定為 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>, ，表示客戶設定檔。 您不應移除的值為設定檔 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> 的 <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>。  
  
5.  呼叫 <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> 方法以移除此物件代表伺服器的使用者定義設定檔。  
  
##  <a name="FollowUp"></a> 後續操作：在變更代理程式參數之後  
 代理程式參數變更會在代理程式下次啟動時生效。 如果代理程式連續執行，則必須停止代理程式，然後重新啟動它。  
  
## 另請參閱  
 [複寫代理程式設定檔](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [複寫快照集代理程式](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [複寫記錄讀取器代理程式](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [複寫散發代理程式](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [複寫合併代理程式](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [複寫佇列讀取器代理程式](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  