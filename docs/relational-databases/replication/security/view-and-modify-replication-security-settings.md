---
title: "檢視及修改複寫安全性設定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modifying replication security settings"
  - "replication [SQL Server], security"
  - "security [SQL Server replication], viewing settings"
  - "viewing replication security settings"
  - "安全性 [SQL Server 複寫], 修改設定"
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 檢視及修改複寫安全性設定
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中檢視及修改複寫安全性設定。 例如，您可能要將「記錄讀取器代理程式」到「發行者」的連接從 SQL Server 驗證變更為 Windows 整合式驗證，或者在 Windows 帳戶密碼變更後，可能需要變更用來執行代理程式作業的認證。 每個代理程式所需的權限的相關資訊，請參閱 [複寫代理程式安全性模型](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要檢視及修改複寫安全性設定，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
-   **待處理︰**  [修改複寫安全性設定之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您所使用的預存程序，將取決於代理程式的類型和伺服器連接的類型而定。  
  
-   您所使用的 RMO 類別和屬性，將取決於代理程式的類型和伺服器連接的類型而定。  
  
###  <a name="Security"></a> 安全性  
 基於安全性理由，密碼的實際值在複寫預存程序所傳回的結果集中會有遮罩。  
  
####  <a name="Permissions"></a> Permissions  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 檢視並修改下列對話方塊中的安全性設定：  
  
1.  **[更新複寫密碼]** 對話方塊，可從 **的** [複寫] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]資料夾開啟。 如果變更複寫拓撲中伺服器上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶或 Windows 帳戶的密碼，請使用此對話方塊，而非更新使用該帳戶之每個代理程式的密碼。 如果多個伺服器上的代理程式使用同一個帳戶，則必須連接到每個伺服器並變更密碼。 密碼在複寫使用密碼的所有位置更新。 而並不會在其他位置更新，例如連結的伺服器。  
  
2.   **代理程式安全性** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
3.   **訂閱屬性-\< 訂閱>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)＞。  
  
4.   **散發者屬性-\< 散發者>** 和 **散發資料庫屬性-\< 資料庫>** 對話方塊。 如需存取這些對話方塊的詳細資訊，請參閱＜ [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)＞。  
  
5.   **發行者屬性-\< 發行者>** 對話方塊。 如需存取此對話方塊的詳細資訊，請參閱＜ [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)＞。  
  
#### 若要變更一個或多個代理程式使用的帳戶之密碼  
  
1.  如果該帳戶是 SQL Server 帳戶，則此對話方塊要變更 SQL Server 帳戶的密碼。 如果該帳戶是 Windows 帳戶，則應先變更 Windows 中的密碼。 如需詳細資訊，請參閱 Windows 文件集。  
  
    > [!NOTE]  
    >  在變更複寫密碼之後，必須停止並重新啟動使用該代理程式變更生效前所用密碼的每一個代理程式。  
  
2.  連接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的伺服器，然後展開伺服器節點。  
  
3.  以滑鼠右鍵按一下 **複寫** 資料夾，然後再按一下 **更新複寫密碼**。  
  
4.  在 **[更新複寫密碼]** 對話方塊中，指定帳戶與新密碼。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 變更快照集代理程式的安全性設定  
  
1.  在 **代理程式安全性** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **安全性設定** 旁 **快照集代理程式** 文字方塊。  
  
2.  在 **[快照集代理程式安全性]** 對話方塊中，指定代理程式執行時所使用的帳戶：  
  
    -   在 **[代理程式帳戶]** 文字方塊中輸入新的 Windows 帳戶。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
3.  指定代理程式要從散發者連接到發行者的內容。 若您選取 **[使用下列的 SQL Server 登入]**，必須同時指定登入：  
  
    -   在 **[登入]** 文字方塊中輸入登入。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
    > [!NOTE]  
    >  如果發行者是 Oracle 發行者 」，指定連接內容 **散發者屬性-\< 散發者>**對話方塊。 請參閱下面用於變更內容的程序。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 變更記錄讀取器代理程式的安全性設定  
  
1.  在 **代理程式安全性** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，按一下 [ **安全性設定** 旁 **記錄讀取器代理程式** 文字方塊。  
  
2.  在 **[記錄讀取器代理程式安全性]** 對話方塊中，指定代理程式執行時所使用的帳戶：  
  
    -   在 **[代理程式帳戶]** 文字方塊中輸入新的 Windows 帳戶。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
3.  指定代理程式要從散發者連接到發行者的內容。 若您選取 **[使用下列的 SQL Server 登入]**，必須同時指定登入：  
  
    -   在 **[登入]** 文字方塊中輸入登入。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
    > [!NOTE]  
    >  如果發行者是 Oracle 發行者 」，指定連接內容 **散發者屬性-\< 散發者>**對話方塊。 使用下一個程序變更內容。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每個已發行的資料庫都有一個「記錄讀取器代理程式」。 在一個發行集上變更代理程式的安全性設定會影響該發行集資料庫中所有發行集的設定。  
  
#### 若要變更 Oracle 發行集的快照集代理程式與記錄讀取器代理程式連接到發行者所使用的內容  
  
1.  在 **發行者** 頁面 **散發者屬性-\< 散發者>** 對話方塊方塊中，按一下 [內容] 按鈕 (**...**) 發行者旁。  
  
2.  在 **[代理程式至發行者的連接]** 區段，指定您設定的複寫管理使用者結構描述所使用之登入與密碼。 如需詳細資訊，請參閱 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 變更發送訂閱之散發代理程式的安全性設定  
  
1.  在 **訂閱屬性-\< 訂閱>** ] 對話方塊中，您可以在發行者上，進行下列變更︰  
  
    -   若要變更的 「 散發代理程式執行和連接到散發者的帳戶，請按一下 [ **代理程式處理帳戶** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[散發代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
    -   若要變更 「 散發代理程式連接到訂閱者的內容，請按一下 [ **訂閱者連接** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
         若您使用佇列更新訂閱，佇列讀取器代理程式亦使用此處指定的內容，連接到訂閱者。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 變更提取訂閱之散發代理程式的安全性設定  
  
1.  在 **訂閱屬性-\< 訂閱>** ] 對話方塊中，您可以在訂閱者 」，進行下列變更︰  
  
    -   若要變更的帳戶的 「 散發代理程式執行和連接到訂閱者，請按一下 [ **代理程式處理帳戶** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[散發代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
         若您使用佇列更新訂閱，佇列讀取器代理程式亦使用此處指定的內容，連接到訂閱者。  
  
    -   若要變更 「 散發代理程式連接到散發者的內容，請按一下 [ **散發者連接** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 變更發送訂閱之合併代理程式的安全性設定  
  
1.  在 **訂閱屬性-\< 訂閱>** ] 對話方塊中，您可以在發行者上，進行下列變更︰  
  
    -   若要變更的合併代理程式執行和連接到發行者與散發者的帳戶，請按一下 [ **代理程式處理帳戶** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[合併代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
    -   若要變更 「 合併代理程式連接到訂閱者的內容，請按一下 [ **訂閱者連接** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 變更提取訂閱之合併代理程式的安全性設定  
  
1.  在 **訂閱屬性-\< 訂閱>** ] 對話方塊中，您可以在訂閱者 」，進行下列變更︰  
  
    -   若要變更的合併代理程式執行和連接到訂閱者的帳戶，請按一下 [ **代理程式處理帳戶** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[合併代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
    -   若要變更 「 合併代理程式連接到發行者與散發者的內容，請按一下 [ **發行者連接** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要變更佇列讀取器代理程式執行時所使用的帳戶  
  
1.  在 **一般** 頁面 **散發者屬性-\< 散發者>** 對話方塊方塊中，按一下 [內容 (**...**) 散發資料庫旁邊的按鈕。  
  
2.  在 **散發資料庫屬性-\< 資料庫>** 對話方塊中，按一下 [ **安全性設定** 旁 **代理程式處理帳戶** 文字方塊。  
  
3.  在 **[佇列讀取器代理程式安全性]** 對話方塊中，指定代理程式執行和連接到「散發者」時所使用的帳戶：  
  
    -   在 **[處理帳戶]** 文字方塊中輸入新的 Windows 帳戶。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每個散發資料庫都會有一個佇列讀取器代理程式。 變更此代理程式的安全性設定時，會影響使用此散發資料庫之所有發行者上的所有發行集設定。  
  
#### 若要變更佇列讀取器代理程式連接到發行者所使用的內容  
  
1.  在 **發行者** 頁面 **散發者屬性-\< 散發者>** 對話方塊方塊中，按一下 [內容] 按鈕 (**...**) 「 發行者 」 旁邊。  
  
2.  在 **[代理程式至發行者的連接 ]** 區段，指定 **[代理程式連接模式]** 選項中 **[模擬代理程式處理帳戶]** 或 **[SQL Server 驗證]** 的值。 如果指定 **[SQL Server 驗證]**，還要輸入 **[登入]** 與 **[密碼]**的值。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每個散發資料庫都會有一個佇列讀取器代理程式。 變更此代理程式的安全性設定時，會影響使用此散發資料庫之所有發行者上的所有發行集設定。  
  
#### 若要變更佇列讀取器代理程式連接到訂閱者所使用的內容  
  
-   「佇列讀取器代理程式」使用與「散發代理程式」相同的連接內容進行訂閱。 如需詳細資訊，請參閱「散發代理程式」的上述程序。  
  
#### 若要變更立即更新提取訂閱的安全性設定  
  
1.  在 **訂閱屬性-\< 訂閱>** 對話方塊在訂閱者上，按一下 [ **發行者連接** 資料列，然後按一下 [內容 (**...**) 的資料列中的按鈕。  
  
2.  在 **[輸入連接資訊]** 對話方塊中，選取下列其中一個選項：  
  
    -   **[使用連結伺服器或遠端伺服器的登入]**。 選取此選項，如果您已經定義遠端伺服器或 「 訂閱者 」 與 「 發行者 」 使用之間的連結的伺服器 [sp_addserver & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), ，[sp_addlinkedserver & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), ，[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ，或另一種方法。  
  
    -   **[利用下列登入和密碼來使用 SQL Server 驗證]**。 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫將為您建立連結的伺服器。 您必須指定已存在於發行者的帳戶。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  此程序會變更複寫觸發程序在「訂閱者」端發生變更時，用來從「訂閱者」連接到「發行者」的方法。 您也可以變更立即更新訂閱之與「散發代理程式」相關的設定。 如需詳細資訊，請參閱本主題前文中的程序。  
>   
>  此程序僅適用於提取訂閱。 對於發送訂閱，請使用預存程序 [sp_link_publication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。  
  
#### 變更從發行者到散發者之管理連接的密碼  
  
1.  上 **發行者** 頁面 **散發者屬性-\< 散發者>** ] 對話方塊中，輸入強式密碼 **密碼** 和 **確認密碼** 文字方塊。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  上 **一般** 頁面 **發行者屬性-\< 發行者>** ] 對話方塊中，輸入強式密碼 **密碼** 和 **確認密碼** 文字方塊。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
> [!IMPORTANT]  
>  在下列所有的程序中，會在可能的情況下，於執行階段提示使用者輸入安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。  
  
#### 變更複寫伺服器上儲存的所有密碼執行個體  
  
1.  在 master 資料庫上的複寫拓撲中的伺服器，執行 [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md)。 針對 [!INCLUDE[msCoName](../../../includes/msCoName-md.md)] @login [!INCLUDE[msCoName](../../../includes/msCoName-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssNoVersion-md.md)] Windows 帳戶或 **@login** 登入，並針對 **@password**。 這樣會變更當連接到拓撲中的其他伺服器時，由此伺服器上的所有代理程式所使用的每一個密碼執行個體。  
  
    > [!NOTE]  
    >  只變更登入和密碼連接到特定伺服器在拓撲中 （例如 「 散發者 」 或 「 訂閱者 」），指定此伺服器的名稱 **@server**。  
  
2.  在必須更新密碼的複寫拓撲中，於每一部伺服器上重複步驟 1。  
  
    > [!NOTE]  
    >  在變更複寫密碼之後，必須停止並重新啟動使用該代理程式變更生效前所用密碼的每一個代理程式。  
  
#### 變更快照集代理程式的安全性設定  
  
1.  在 「 發行者 」 執行 [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), ，並指定 **@publication**。 這樣會傳回快照集代理程式目前的安全性設定。  
  
2.  在 「 發行者 」 執行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), ，並指定 **@publication** 和一或多個下列安全性設定來變更︰  
  
    -   若要變更之 Windows 帳戶指定代理程式執行，或只是這個帳戶密碼， **@job_login** 和 **@job_password**。  
  
    -   若要變更連接到發行者時使用的安全性模式，指定其值為 **1** 或 **0** 的 **@publisher_security_mode**。  
  
    -   當連接到發行者時使用的安全性模式變更 **1** 至 **0** ，或變更 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用於此連接的登入，請指定 **@publisher_login** 和 **@publisher_password**。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 變更記錄讀取器代理程式的安全性設定  
  
1.  在 「 發行者 」 執行 [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md), ，並指定 **@publisher**。 這樣會傳回記錄讀取器代理程式目前的安全性設定。  
  
2.  在 「 發行者 」 執行 [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md), ，並指定 **@publication** 和一或多個下列安全性設定來變更︰  
  
    -   若要變更之 Windows 帳戶指定代理程式執行，或只是這個帳戶密碼， **@job_login** 和 **@job_password**。  
  
    -   若要變更連接到發行者時使用的安全性模式，指定其值為 **1** 或 **0** 的 **@publisher_security_mode**。  
  
    -   當連接到發行者時使用的安全性模式變更 **1** 至 **0** ，或變更 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用於此連接的登入，請指定 **@publisher_login** 和 **@publisher_password**。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 變更發送訂閱之散發代理程式的安全性設定  
  
1.  在發行集資料庫的發行者，執行 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md), ，並指定 **@publication** 和 **@subscriber**。 這樣會傳回訂閱屬性，包括在散發者上執行之散發代理程式的安全性設定。  
  
2.  在發行集資料庫的發行者，執行 [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md), ，並指定 **@publication**, ，**@subscriber**, ，**@subscriber_db**, ，值為 **所有** 的 **@article**, ，安全性屬性的名稱 **@property**, ，與新值之屬性的 **@value**。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   此帳戶的密碼變更的 Windows 帳戶底下執行代理程式，或只是指定其值為 **distrib_job_password** 的 **@property** 和新密碼 **@value**。 在變更此帳戶本身，請重複步驟 2 指定的值為 **distrib_job_login** 的 **@property** 和新的 Windows 帳戶，以便 **@value**。  
  
    -   若要變更連接到 「 訂閱者 」 時使用的安全性模式，指定其值為 **subscriber_security_mode** 的 **@property** 且值為 **1** （Windows 整合式驗證） 或 **0** （SQL Server 驗證） 的 **@value**。  
  
    -   當訂閱者的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證登入資訊，請指定其值為 **subscriber_password** 的 **@property** 和新密碼 **@value**。 指定的值重複步驟 2， **subscriber_login** 的 **@property** 和新的登入的 **@value**。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有屬性的值來設定發行者時包括 **distrib_job_login** 和 **distrib_job_password**, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 變更提取訂閱之散發代理程式的安全性設定  
  
1.  在 「 訂閱者 」 執行 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md), ，並指定 **@publication**。 這樣會傳回訂閱屬性，包括在訂閱者上執行之散發代理程式的安全性設定。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), ，並指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，安全性屬性的名稱 **@property**, ，與新值之屬性的 **@value**。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   此帳戶的密碼變更的 Windows 帳戶底下執行代理程式，或只是指定其值為 **distrib_job_password** 的 **@property** 和新密碼 **@value**。 在變更此帳戶本身，請重複步驟 2 指定的值為 **distrib_job_login** 的 **@property** 和新的 Windows 帳戶，以便 **@value**。  
  
    -   若要變更連接到散發者時使用的安全性模式，指定其值為 **distributor_security_mode** 的 **@property** 且值為 **1** （Windows 整合式驗證） 或 **0** （SQL Server 驗證） 的 **@value**。  
  
    -   當散發者的安全性模式變更為 SQL Server 驗證或變更 SQL Server 驗證登入資訊，請指定其值為 **distributor_password** 的 **@property** 和新密碼 **@value**。 指定的值重複步驟 2， **distributor_login** 的 **@property** 和新的登入的 **@value**。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
#### 變更發送訂閱之合併代理程式的安全性設定  
  
1.  在發行集資料庫的發行者，執行 [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md), ，並指定 **@publication**, ，**@subscriber**, ，和 **@subscriber_db**。 這樣會傳回訂閱屬性，包括在散發者上執行之合併代理程式的安全性設定。  
  
2.  在發行集資料庫的發行者，執行 [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md), ，並指定 **@publication**, ，**@subscriber**, ，**@subscriber_db**, ，安全性屬性的名稱 **@property**, ，與新值之屬性的 **@value**。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   此帳戶的密碼變更的 Windows 帳戶，代理程式上執行，或只是指定其值為 **merge_job_password** 的 **@property** 和新密碼 **@value**。 在變更此帳戶本身，請重複步驟 2 指定的值為 **merge_job_login** 的 **@property** 和新的 Windows 帳戶，以便 **@value**。  
  
    -   若要變更連接到 「 訂閱者 」 時使用的安全性模式，指定其值為 **subscriber_security_mode** 的 **@property** 且值為 **1** （Windows 整合式驗證） 或 **0** （SQL Server 驗證） 的 **@value**。  
  
    -   當訂閱者的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證登入資訊，請指定其值為 **subscriber_password** 的 **@property** 和新密碼 **@value**。 指定的值重複步驟 2， **subscriber_login** 的 **@property** 和新的登入的 **@value**。  
  
    -   若要變更連接到發行者時使用的安全性模式，指定其值為 **publisher_security_mode** 的 **@property** 且值為 **1** （Windows 整合式驗證） 或 **0** （SQL Server 驗證） 的 **@value**。  
  
    -   當 「 發行者 」 的安全性模式變更為 「 SQL Server 驗證，或變更 SQL Server 驗證登入資訊，請指定其值為 **publisher_password** 的 **@property** 和新密碼 **@value**。 指定的值重複步驟 2， **publisher_login** 的 **@property** 和新的登入的 **@value**。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有屬性的值來設定發行者時包括 **merge_job_login** 和 **merge_job_password**, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 變更提取訂閱之合併代理程式的安全性設定  
  
1.  在 「 訂閱者 」 執行 [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md), ，並指定 **@publication**。 這樣會傳回訂閱屬性，包括在訂閱者上執行之合併代理程式的安全性設定。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), ，並指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，安全性屬性的名稱 **@property**, ，與新值之屬性的 **@value**。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   此帳戶的密碼變更的 Windows 帳戶底下執行代理程式，或只是指定其值為 **merge_job_password** 的 **@property** 和新密碼 **@value**。 當變更此帳戶本身，重複步驟 2 指定的值為 **merge_job_login** 的 **@property** 和新的 Windows 帳戶，以便 **@value**。  
  
    -   若要變更連接到散發者時使用的安全性模式，指定其值為 **distributor_security_mode** 的 **@property** 且值為 **1** （Windows 整合式驗證） 或 **0** （SQL Server 驗證） 的 **@value**。  
  
    -   當散發者的安全性模式變更為 SQL Server 驗證或變更 SQL Server 驗證登入資訊，請指定其值為 **distributor_password** 的 **@property** 和新密碼 **@value**。 指定的值重複步驟 2， **distributor_login** 的 **@property** 和新的登入的 **@value**。  
  
    -   若要變更連接到發行者時使用的安全性模式，指定其值為 **publisher_security_mode** 的 **@property** 且值為 **1** （Windows 整合式驗證） 或 **0** （SQL Server 驗證） 的 **@value**。  
  
    -   當 「 發行者 」 的安全性模式變更為 「 SQL Server 驗證或變更 SQL Server 驗證登入資訊，指定其值為 **publisher_password** 的 **@property** 和新密碼 **@value**。 指定的值重複步驟 2， **publisher_login** 的 **@property** 和新的登入的 **@value**。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
#### 變更快照集代理程式的安全性設定，為訂閱者產生篩選過的快照集  
  
1.  在 「 發行者 」 執行 [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md), ，並指定 **@publication**。 在結果集，請記下的值 **job_name** 若要變更的訂閱者的資料分割。  
  
2.  在 「 發行者 」 執行 [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md), ，並指定 **@publication**, ，步驟 1 中取得的值 **@dynamic_snapshot_jobname**, ，和新密碼 **@job_password** 登入和密碼的代理程式執行的 Windows 帳戶或 **@job_login** 和 **@job_password**。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者，提供給所有參數的值來設定發行者時包括 *job_login* 和 *job_password*, ，傳送到 「 散發者 」，以純文字。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱 [啟用加密連接 Database Engine & #40。SQL Server 組態管理員 & #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 變更佇列讀取器代理程式的安全性設定  
  
1.  在散發者 」 執行 [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)。 這樣會傳回佇列讀取器代理程式執行時所用的目前 Windows 帳戶。  
  
    -   在散發者 」 執行 [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md), ，指定 Windows 帳戶設定 **@job_login** 和 **@job_passwsord**。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。 每個散發資料庫都會有一個佇列讀取器代理程式。 變更此代理程式的安全性設定時，會影響使用此散發資料庫之所有發行者上的所有發行集設定。  
  
2.  佇列讀取器代理程式會使用與訂閱之散發代理程式相同的連接內容連接到訂閱者。  
  
#### 變更立即更新訂閱者連接到發行者時所用的安全性模式  
  
1.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。 指定 **@publisher**, ，**@publication**, ，發行集資料庫的名稱 **@publisher_db**, ，和下列其中一個值 **@security_mode**:  
  
    -   **0** - 在發行者上進行更新時使用「SQL Server 驗證」。 此選項要求您在發行者上指定對 **@login** 和 **@password**有效的登入。  
  
    -   **1** - 在連接到發行者時，使用在訂閱者上進行變更之使用者的安全性內容。 請參閱 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 與此安全性模式有關的限制。  
  
    -   **2** 若要使用的現有，使用者定義連結伺服器登入使用建立 [sp_addlinkedserver & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)。  
  
#### 變更遠端散發者的密碼  
  
1.  在散發資料庫的散發者端，執行 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), ，指定此登入的新密碼 **@password**。  
  
    > [!IMPORTANT]  
    >  未變更的密碼 **distributor_admin** 直接。  
  
2.  在每個使用此遠端散發者的發行者，執行 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), ，指定步驟 1 中的密碼 **@password**。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。  
  
#### 變更複寫伺服器上儲存的所有密碼執行個體  
  
1.  建立複寫伺服器的連接使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別使用步驟 1 中的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> 方法。 指定下列參數：  
  
    -   *security_mode* - <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> 值，指定變更密碼的所有執行個體的驗證類型。  
  
    -   *登入* -變更所有密碼執行個體的登入。  
  
    -   *密碼* -新的密碼值。  
  
        > [!IMPORTANT]  
        >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 Windows .NET Framework 提供的 [密碼編譯服務](http://go.microsoft.com/fwlink/?LinkId=34733) 。  
  
        > [!NOTE]  
        >  只有成員 **sysadmin** 固定的伺服器角色可以呼叫這個方法。  
  
4.  在必須更新密碼的複寫拓撲中，於每一部伺服器上重複步驟 1-3。  
  
#### 針對交易式發行集的發送訂閱變更散發代理程式的安全性設定  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 屬性的訂閱，並將連接從步驟 1 的設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  執行個體上設定一或多個下列的安全性內容 <xref:Microsoft.SqlServer.Replication.TransSubscription>:  
  
    -   若要變更執行代理程式的 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   指定 Windows 整合式驗證的代理程式連接到訂閱者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 屬性 **，則為 true**。  
  
    -   指定 SQL Server 驗證的代理程式連接到訂閱者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 屬性 **false**, ，並指定的訂閱者登入認證 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位。  
  
        > [!NOTE]  
        >  代理程式連接到散發者一定會使用指定的 Windows 認證 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
#### 針對交易式發行集的提取訂閱變更散發代理程式的安全性設定  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性的訂閱，並將連接從步驟 1 的設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  執行個體上設定一或多個下列的安全性內容 <xref:Microsoft.SqlServer.Replication.TransPullSubscription>:  
  
    -   若要變更執行代理程式的 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   指定 Windows 整合式驗證的代理程式連接到散發者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 屬性 **，則為 true**。  
  
    -   指定 SQL Server 驗證的代理程式連接到散發者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 屬性 **false**, ，指定散發者登入認證 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位。  
  
        > [!NOTE]  
        >  代理程式連接到訂閱者一定會使用指定的 Windows 認證 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
#### 針對合併式發行集的提取訂閱變更合併代理程式的安全性設定  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性的訂閱，並將連接從步驟 1 的設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  執行個體上設定一或多個下列的安全性內容 <xref:Microsoft.SqlServer.Replication.MergePullSubscription>:  
  
    -   若要變更執行代理程式的 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   指定 Windows 整合式驗證的代理程式連接到散發者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 屬性 **，則為 true**。  
  
    -   指定 SQL Server 驗證的代理程式連接到散發者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 屬性 **false**, ，指定散發者登入認證 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位。  
  
    -   指定 Windows 整合式驗證的代理程式連接到發行者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 屬性 **，則為 true**。  
  
    -   指定 SQL Server 驗證的代理程式連接到發行者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 屬性 **false**, ，並指定的發行者登入認證 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位。  
  
        > [!NOTE]  
        >  代理程式連接到訂閱者一定會使用指定的 Windows 認證 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
#### 針對合併式發行集的發送訂閱變更合併代理程式的安全性設定  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別。  
  
3.  設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 屬性的訂閱，並將連接從步驟 1 的設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  執行個體上設定一或多個下列的安全性內容 <xref:Microsoft.SqlServer.Replication.MergeSubscription>:  
  
    -   若要變更執行代理程式的 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 欄位 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   指定 Windows 整合式驗證的代理程式連接到訂閱者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 屬性 **，則為 true**。  
  
    -   指定 SQL Server 驗證的代理程式連接到訂閱者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 屬性 **false**, ，並指定的訂閱者登入認證 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位。  
  
    -   指定 Windows 整合式驗證的代理程式連接到發行者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 屬性 **，則為 true**。  
  
    -   指定 SQL Server 驗證的代理程式連接到發行者時所使用的驗證類型，請設定 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 欄位 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 屬性 **false**, ，並指定的發行者登入認證 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> 欄位。  
  
        > [!NOTE]  
        >  代理程式連接到散發者一定會使用指定的 Windows 認證 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  （選擇性）如果您指定的值 **true** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您指定的值 **false** 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （預設值），變更會立即傳送至伺服器。  
  
#### 變更立即更新訂閱者連接到交易式發行者時所用的登入資訊  
  
1.  建立連接到訂閱者使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 訂閱資料庫的類別。 指定 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的資料庫屬性定義不正確，或者此訂閱資料庫不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> 方法，傳遞下列參數︰  
  
    -   *發行者* -發行者的名稱。  
  
    -   *PublisherDB* -發行集資料庫的名稱。  
  
    -   *發行集* -立即更新訂閱者訂閱的發行集名稱。  
  
    -   *散發者* -散發者的名稱。  
  
    -   *PublisherSecurity* - <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> 物件，指定使用立即更新訂閱者連接到發行者與登入認證的連接時的安全性模式類型。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 這個範例會檢查提供的登入值，並針對提供的 Windows 登入或 SQL Server 登入 (在伺服器上由複寫儲存) 變更其所有密碼。  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> 後續操作：在您修改複寫安全性設定之後  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## 另請參閱  
 [Replication Management Objects 概念。](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [升級複寫指令碼 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [管理複寫的登入與密碼](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫安全性最佳做法](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保護 & #40。複寫 & #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  