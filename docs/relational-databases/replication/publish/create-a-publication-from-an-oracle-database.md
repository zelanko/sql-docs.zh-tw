---
title: 從 Oracle 資料庫建立發行集 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], Oracle databases
- Oracle publishing [SQL Server replication], configuring
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cdb8847a7aaf7aaa9b21a64ed6736738da6df9dc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882211"
---
# <a name="create-a-publication-from-an-oracle-database"></a>從 Oracle 資料庫建立發行集
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中從 Oracle 資料庫建立發行集。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [先決條件](#Prerequisites)  
  
-   **若要從 Oracle 資料庫建立發行集，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
  
-   建立發行集之前，您必須先在「[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」上安裝 Oracle 軟體，也必須設定 Oracle 資料庫。 如需詳細資訊，請參閱[設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用「新增發行集精靈」從「Oracle 資料庫」建立快照式或交易式發行集。  
  
 第一次從 Oracle 資料庫建立發行集時，必須在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端識別「Oracle 發行者」(如果是同一資料庫的後續發行集，則不需要執行這個動作)。 可從 [新增發行集精靈] 或 [散發者屬性 - \<Distributor>] 對話方塊來完成 Oracle 發行者的識別；本主題會顯示 [散發者屬性 - \<Distributor>] 對話方塊。  
  
#### <a name="to-identify-the-oracle-publisher-at-the-sql-server-distributor"></a>若要在 SQL Server 散發者端識別 Oracle 發行者  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中，連接到「Oracle 發行者」將其做為「散發者」使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]** 資料夾，然後按一下 **[散發者屬性]** 。  
  
3.  在 [散發者屬性 - \<Distributor>] 對話方塊的 [發行者] 頁面上，按一下 [新增]，然後按一下 [新增 Oracle 發行者]。  
  
4.  在 **[連接到伺服器]** 對話方塊上，按一下 **[選項]** 按鈕。  
  
5.  在 **[登入]** 索引標籤上：  
  
    1.  在 **[伺服器執行個體]** 下拉式方塊中輸入 Oracle 資料庫執行個體名稱或選取 **[瀏覽其他]** 。  
  
    2.  選取 **[Oracle 標準驗證]** (建議選項) 或 **[Windows 驗證]** 。  
  
         如果您選取 **[Windows 驗證]** ：必須使用 Windows 認證將 Oracle 伺服器設定為允許連接 (如需詳細資訊，請參閱 Oracle 文件集)；並且您的目前登入帳戶必須與您為複寫管理的使用者結構描述指定的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帳戶相同。  
  
    3.  如果您選取 **[Oracle 標準驗證]** ，則於設定期間輸入您在「Oracle 發行者」上建立的複寫管理使用者結構描述之登入和密碼。  
  
6.  在 **[連接屬性]** 索引標籤上，選取 **[閘道]** 或 **[完整]** 的「發行者」類型。  
  
     **[完整]** 選項可以為 Oracle 發行提供具有完整支援功能的快照式和交易式發行集。 **[閘道]** 選項可以在複寫作為系統之間的閘道時，提供特定的設計最佳化以提升效能。 如果您計畫在多個交易式發行集內發行相同的資料表，就無法使用 **[閘道]** 選項。 如果您選取 **[閘道]** ，則資料表最多只能在一個交易式發行集裡出現，但可以在任意數目的快照式發行集裡出現。  
  
7.  按一下 **[連接]** ，建立與「Oracle 發行者」的連接，並為複寫設定該連接。 [連線到伺服器] 對話方塊隨即關閉，並會將您返回至 [散發者屬性 - \<Distributor>] 對話方塊。  
  
    > [!NOTE]  
    >  如果網路組態有問題，此時您會收到一條錯誤訊息。 如果您遇到連接到 Oracle 資料庫的問題，請參閱在＜ [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)＞中的「SQL Server 散發者無法連接到 Oracle 資料庫執行個體」一節。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

#### <a name="to-create-a-publication-from-an-oracle-database"></a>若要從 Oracle 資料庫建立發行集  
  
1.  連接到「Oracle 發行者」將其做為「散發者」使用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾。  
  
3.  以滑鼠右鍵按一下 **[本機發行集]** 資料夾，然後按一下 **[新增 Oracle 發行集]** 。  
  
4.  在「新增發行集精靈」的 **[Oracle 發行者]** 頁面，選取「Oracle 發行者」。 如果「Oracle 發行者」未顯示，按一下 **[新增 Oracle 發行者]** ，這會引領您繼續先前程序之後的步驟。  
  
5.  在 **[發行集類型]** 頁面上，選取 **[快照集發行集]** 或 **[交易式發行集]** 。  
  
6.  在 **[發行項]** 頁面上，選取您要發行的資料庫物件。  
  
     或者，透過展開資料表，然後清除一個或多個資料行之核取方塊的方式，篩選出資料表的資料行。 如有必要，按一下 **[發行項屬性]** 以檢視和修改發行項屬性，並指定替代資料類型對應。 若要指定資料類型對應的詳細資訊，請參閱[指定 Oracle 發行者的資料類型對應](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)。  
  
7.  在 **[篩選資料表的資料列]** 頁面，選擇性地套用篩選以發行一個或多個資料表的資料子集。  
  
8.  僅當在訂閱資料庫中已建立了所有物件，且已加入了所有需要的資料時，才能在 **[快照集代理程式]** 頁面清除 **[立即建立快照集]** 。  
  
9. 在 **[代理程式安全性]** 頁面，指定「快照集代理程式」的認證 (針對所有發行集) 和「記錄讀取器代理程式」的認證 (針對交易式發行集)。 代理程式會使用您指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows 帳戶之內容，執行並與「 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 散發者」建立連接。 代理程式會使用您指定為複寫管理使用者結構描述的帳戶內容，與 Oracle 資料庫建立連接。 如需詳細資訊，請參閱[設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
     如需各代理程式所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) ＞和＜ [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)＞。  
  
10. 在 **[精靈動作]** 頁面上，選擇性地為發行集編寫指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
11. 在 **[完成精靈]** 頁面上，指定發行集的名稱。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 當 Oracle 資料庫已經設定為發行者之後，您可以使用系統預存程序來建立交易式或快照式發行集，就像是從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者建立一樣。  
  
#### <a name="to-create-an-oracle-publication"></a>建立 Oracle 發行集  
  
1.  將 Oracle 資料庫設定為發行者。 如需詳細資訊，請參閱[設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
2.  如果遠端散發者不存在，請設定遠端散發者。 如需詳細資訊，請參閱 [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md)。  
  
3.  在 Oracle 發行者將使用的遠端散發者端，執行 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 資料庫執行個體的透明網路基質 (Transparent Network Substrate，TNS) 名稱，並針對 **\@publisher_type** 指定 **ORACLE** 或 **ORACLE GATEWAY** 值。 `Specify` 指定當從 Oracle 發行者連接到遠端 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者時所使用的安全性模式，如下列其中一項：  
  
    -   若要使用預設值 Oracle 標準驗證，請將 **\@security_mode** 指定為 **0** 值、將 **\@login** 指定為設定期間您在 Oracle 發行者上所建立複寫管理使用者結構描述的登入，並為 **\@password** 指定密碼。  
  
        > [!IMPORTANT]  
        >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。  
  
    -   若要使用 Windows 驗證，請將 **\@security_mode** 指定為 **1** 值。  
  
        > [!NOTE]  
        >  若要使用「Windows 驗證」，必須使用 Windows 認證將 Oracle 伺服器設定為允許連接 (如需詳細資訊，請參閱 Oracle 文件集)；並且您目前的登入帳戶必須與您為複寫管理使用者結構描述指定的 Microsoft Windows 帳戶相同。  
  
4.  針對發行集資料庫建立記錄讀取器代理程式作業。  
  
    -   如果您不確定發行的資料庫是否有記錄讀取器代理程式作業存在，請在散發資料庫上由 Oracle 發行者使用的散發者端執行 [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者的名稱。 如果結果集是空的，就必須建立記錄讀取器代理程式作業。  
  
    -   如果記錄讀取器代理程式作業已存在發行集資料庫中，請繼續進行步驟 5。  
  
    -   在散發資料庫上由 Oracle 發行者使用的散發者端，執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 針對 **\@job_login** 和 **\@job_password** 指定此代理程式執行時所用的 Windows 認證。  
  
        > [!NOTE]  
        >  **\@job_login** 參數必須符合步驟 3 中所提供的登入。 請勿提供發行者安全性資訊。 記錄讀取器代理程式會使用步驟 3 中所提供的安全性資訊連接到發行者。  
  
5.  在散發資料庫的散發者端，執行 [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 來建立發行集。 如需詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
6.  在散發資料庫的散發者端，執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 針對 **\@publication** 指定步驟 4 中所使用的發行集名稱，並針對 **\@job_name** 和 **\@password** 指定執行快照集代理程式時所使用的 Windows 認證。 若要在連接到發行者時使用 Oracle 標準驗證，您也必須針對 **\@publisher_security_mode** 指定 **0** 值，並針對 **\@publisher_login** 和 **\@publisher_password** 指定 Oracle 登入資訊。 這麼做會為發行集建立快照集代理程式作業。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [設定 Oracle 發行者的交易集作業 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [授與 Oracle 權限的指令碼](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  
