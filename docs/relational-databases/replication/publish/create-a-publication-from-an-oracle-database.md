---
title: "從 Oracle 資料庫建立發行集 | Microsoft Docs"
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
  - "publications [SQL Server replication], Oracle databases"
  - "Oracle 發行 [SQL Server 複寫], 設定"
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 從 Oracle 資料庫建立發行集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中從 Oracle 資料庫建立發行集。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
-   **若要從 Oracle 資料庫建立發行集，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   建立發行集之前，您必須先在「 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上安裝 Oracle 軟體，還必須設定 Oracle 資料庫。 如需詳細資訊，請參閱 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增發行集精靈」從「Oracle 資料庫」建立快照式或交易式發行集。  
  
 第一次從 Oracle 資料庫建立發行集時，必須在「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端識別「Oracle 發行者」(如果是同一資料庫的後續發行集，則不需要執行這個動作)。 識別 「 Oracle 發行者 」 可以從新增發行集精靈 」 來完成或 **散發者屬性-\< 散發者>** 對話方塊; 本主題顯示 **散發者屬性-\< 散發者>** 對話方塊。  
  
#### 若要在 SQL Server 散發者端識別 Oracle 發行者  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，連接到「Oracle 發行者」將其做為「散發者」使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **複寫** 資料夾，然後再按一下 **散發者屬性**。  
  
3.  在 **發行者** 頁面 **散發者屬性-\< 散發者>** 對話方塊中，按一下 [ **新增**, ，然後按一下 [ **加入 Oracle 發行者**。  
  
4.  在 **[連接到伺服器]** 對話方塊上，按一下 **[選項]** 按鈕。  
  
5.  在 **[登入]** 索引標籤上：  
  
    1.  在 **[伺服器執行個體]** 下拉式方塊中輸入 Oracle 資料庫執行個體名稱或選取 **[瀏覽其他]** 。  
  
    2.  選取 **Oracle 標準驗證** （建議） 或 **Windows 驗證**。  
  
         如果您選取 **Windows 驗證**︰ 在 Oracle 伺服器必須設定為允許使用 Windows 認證進行連接 （如需詳細資訊，請參閱 Oracle 文件）; 您必須是目前登入相同 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 您為複寫管理使用者結構描述指定的 Windows 帳戶。  
  
    3.  如果您選取 **[Oracle 標準驗證]**，則於設定期間輸入您在「Oracle 發行者」上建立的複寫管理使用者結構描述之登入和密碼。  
  
6.  在 **[連接屬性]** 索引標籤上，選取 **[閘道]** 或 **[完整]**的「發行者」類型。  
  
     [完整]  選項可以為 Oracle 發行提供具有完整支援功能的快照式和交易式發行集。 **[閘道]** 選項可以在複寫作為系統之間的閘道時，提供特定的設計最佳化以提升效能。 如果您計畫在多個交易式發行集內發行相同的資料表，就無法使用 **[閘道]** 選項。 如果您選取 **[閘道]**，則資料表最多只能在一個交易式發行集裡出現，但可以在任意數目的快照式發行集裡出現。  
  
7.  按一下 **[連接]**，建立與「Oracle 發行者」的連接，並為複寫設定該連接。  **連接到伺服器** 對話方塊會關閉，而您會回到 **散發者屬性-\< 散發者>** 對話方塊。  
  
    > [!NOTE]  
    >  如果網路組態有問題，此時您會收到一條錯誤訊息。 如果您遇到連接到 Oracle 資料庫的問題，請參閱在＜ [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)＞中的「SQL Server 散發者無法連接到 Oracle 資料庫執行個體」一節。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要從 Oracle 資料庫建立發行集  
  
1.  連接到「Oracle 發行者」將其做為「散發者」使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾。  
  
3.  以滑鼠右鍵按一下 **本機發行集** 資料夾，然後再按一下 **新增 Oracle 發行集**。  
  
4.  在「新增發行集精靈」的 **[Oracle 發行者]** 頁面，選取「Oracle 發行者」。 如果「Oracle 發行者」未顯示，按一下 **[新增 Oracle 發行者]**，這會引領您繼續先前程序之後的步驟。  
  
5.  在 **[發行集類型]** 頁面上，選取 **[快照集發行集]** 或 **[交易式發行集]**。  
  
6.  在 **[發行項]** 頁面上，選取您要發行的資料庫物件。  
  
     或者，透過展開資料表，然後清除一個或多個資料行之核取方塊的方式，篩選出資料表的資料行。 如有必要，按一下 **[發行項屬性]** 以檢視和修改發行項屬性，並指定替代資料類型對應。 如需資料類型對應的詳細資訊，請參閱 [Oracle 發行者指定資料型別對應](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)。  
  
7.  在 **[篩選資料表的資料列]** 頁面，選擇性地套用篩選以發行一個或多個資料表的資料子集。  
  
8.  僅當在訂閱資料庫中已建立了所有物件，且已加入了所有需要的資料時，才能在 **[快照集代理程式]** 頁面清除 **[立即建立快照集]** 。  
  
9. 在 **代理程式安全性** 頁面上，指定快照集代理程式 （適用於所有發行集） 和記錄讀取器代理程式 （針對交易式發行集） 的認證。 代理程式會使用您指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows 帳戶之內容，執行並與「 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 散發者」建立連接。 代理程式會使用您指定為複寫管理使用者結構描述的帳戶內容，與 Oracle 資料庫建立連接。 如需詳細資訊，請參閱 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
     如需各代理程式所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) ＞和＜ [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)＞。  
  
10. 在 **[精靈動作]** 頁面上，選擇性地為發行集編寫指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
11. 在 **[完成精靈]** 頁面上，指定發行集的名稱。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 當 Oracle 資料庫已經設定為發行者之後，您可以使用系統預存程序來建立交易式或快照式發行集，就像是從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者建立一樣。  
  
#### 建立 Oracle 發行集  
  
1.  將 Oracle 資料庫設定為發行者。 如需詳細資訊，請參閱 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
2.  如果遠端散發者不存在，請設定遠端散發者。 如需詳細資訊，請參閱 [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md)。  
  
3.  在 「 Oracle 發行者 」 將會使用遠端散發者 」 執行 [sp_adddistpublisher & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)。 指定 Oracle 資料庫執行個體的 Transparent Network Substrate (TNS) 名稱 **@publisher** 且值為 **ORACLE** 或 **ORACLE GATEWAY** 的 **@publisher_type**。 `Specify` 指定當從 Oracle 發行者連接到遠端 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者時所使用的安全性模式，如下列其中一項：  
  
    -   若要使用 Oracle 標準驗證，預設值，指定其值為 **0** 的 **@security_mode**, ，組態期間在 「 Oracle 發行者 」 建立複寫管理使用者結構描述的登入 **@login**, ，密碼 **@password**。  
  
        > [!IMPORTANT]  
        >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。  
  
    -   若要使用 Windows 驗證，指定其值為 **1** 的 **@security_mode**。  
  
        > [!NOTE]  
        >  若要使用「Windows 驗證」，必須使用 Windows 認證將 Oracle 伺服器設定為允許連接 (如需詳細資訊，請參閱 Oracle 文件集)；並且您目前的登入帳戶必須與您為複寫管理使用者結構描述指定的 Microsoft Windows 帳戶相同。  
  
4.  針對發行集資料庫建立記錄讀取器代理程式作業。  
  
    -   如果您不確定是否記錄讀取器代理程式作業存在已發行的資料庫，執行 [sp_helplogreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 在散發資料庫上的 Oracle 發行者所使用的散發者。 針對 **@publisher**指定 Oracle 發行者的名稱。 如果結果集是空的，就必須建立記錄讀取器代理程式作業。  
  
    -   如果記錄讀取器代理程式作業已存在發行集資料庫中，請繼續進行步驟 5。  
  
    -   在 Oracle 發行者在散發資料庫上使用 「 散發者 」 執行 [sp_addlogreader_agent & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 指定 Windows 認證的代理程式執行 **@job_login** 和 **@job_password**。  
  
        > [!NOTE]  
        >   **@Job_login** 參數必須符合在步驟 3 中所提供的登入。 請勿提供發行者安全性資訊。 記錄讀取器代理程式會使用步驟 3 中所提供的安全性資訊連接到發行者。  
  
5.  在散發資料庫的散發者端，執行 [sp_addpublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 若要建立發行集。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
6.  在散發資料庫的散發者端，執行 [sp_addpublication_snapshot & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定使用步驟 4 中的發行集名稱 **@publication** 和 Windows 認證的快照集代理程式執行 **@job_name** 和 **@password**。 若要連接到發行者時，請使用 Oracle 標準驗證，您也必須指定值為 **0** 的 **@publisher_security_mode** Oracle 登入資訊和 **@publisher_login** 和 **@publisher_password**。 這麼做會為發行集建立快照集代理程式作業。  
  
## 另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Oracle 發行者 & #40; 設定交易集作業複寫 TRANSACT-SQL 程式設計 & #41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md)   
 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [授與 Oracle 權限的指令碼](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  