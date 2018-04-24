---
title: 為非 SQL Server 訂閱者建立訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers, subscriptions
ms.assetid: 5020ee68-b988-4d57-8066-67d183e61237
caps.latest.revision: 28
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70d890ec5941dd06bc855c23e0de24624d10a27d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-subscription-for-a-non-sql-server-subscriber"></a>為非 SQL Server 訂閱者建立訂閱
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中針對非 SQL Server 訂閱者建立訂閱。 異動複寫與快照式複寫支援向非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者發行資料。 如需有關支援之訂閱者平台的資訊，請參閱＜ [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)中針對非 SQL Server 訂閱者建立訂閱。  
  
 **本主題內容**  
  
-   **若要針對非 SQL Server 訂閱者建立訂閱，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 若要為非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者建立訂閱：  
  
1.  在「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 散發者」上安裝並設定適當的用戶端軟體和 OLE DB 提供者。 如需相關資訊，請參閱 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) 及 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)。  
  
2.  使用「新增發行集精靈」建立發行集。 如需建立發行集的詳細資訊，請參閱[建立發行集](../../relational-databases/replication/publish/create-a-publication.md)和[從 Oracle 資料庫建立發行集](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。 在「新增發行集精靈」中指定下列選項：  
  
    -   在 **[發行集類型]** 頁面上，選取 **[快照集發行集]** 或 **[交易式發行集]**。  
  
    -   在 **[快照集代理程式]** 頁面上，清除 **[立即建立快照集]**。  
  
         為非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者啟用發行集後建立快照集，以確定「快照集代理程式」會產生適用於非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者的快照集與初始化指令碼。  
  
3.  使用 [發行集屬性 - \<發行集名稱>] 對話方塊，啟用非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者的發行集。 如需有關此步驟的詳細資訊，請參閱＜ [Publication Properties, Subscription Options](../../relational-databases/replication/publication-properties-subscription-options.md) ＞。  
  
4.  使用「新增訂閱精靈」建立訂閱。 本主題提供有關這個步驟的詳細資訊。  
  
5.  (選擇性) 變更 **pre_creation_cmd** 發行項屬性，使資料表保留在訂閱者端。 本主題提供有關這個步驟的詳細資訊。  
  
6.  產生發行集的快照集。 本主題提供有關這個步驟的詳細資訊。  
  
7.  同步處理訂閱。 如需詳細資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### <a name="to-enable-a-publication-for-non-sql-server-subscribers"></a>為非 SQL Server 訂閱者啟用發行集  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下發行集，然後再按一下 **[屬性]**。  
  
4.  在 **[訂閱選項]** 頁面中，為 **[允許非 SQL Server 訂閱者]** 選項選取 **[True]**值。 選取此選項會變更某些屬性，使發行集能與非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者相容。  
  
    > [!NOTE]  
    >  選取 **[True]** 會將 **pre_creation_cmd** 發行項屬性值設為 'drop'。 這項設定會指定當複寫符合發行項中的資料表名稱時，應該要卸除「訂閱者」端的資料表。 如果您在「訂閱者」端有想要保留的現有資料表，請針對每一個發行項使用 [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 預存程序，並為 **pre_creation_cmd**指定 'none' 值： `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 將會提示您為發行集建立新快照集。 如果不想此時建立快照集，請稍後使用下一個「如何」程序中描述的步驟。  
  
#### <a name="to-create-a-subscription-for-a-non-sql-server-subscriber"></a>為非 SQL Server 訂閱者建立訂閱  
  
1.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
2.  以滑鼠右鍵按一下適當的發行集，然後再按一下 **[新增訂閱]**。  
  
3.  在 **[散發代理程式位置]** 頁面中，確定已選取 **[在散發者端執行所有代理程式]** 。 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者不支援在「訂閱者」端執行代理程式。  
  
4.  在 **[訂閱者]** 頁面中，按一下 **[加入訂閱者]** 然後按一下 **[加入非 SQL Server 訂閱者]**。  
  
5.  在 **[加入非 SQL Server 訂閱者]** 對話方塊中，選取「訂閱者」類型。  
  
6.  在 **[資料來源名稱]**中輸入值：  
  
    -   對於 Oracle，該值是您設定的 Transparent Network Substrate (TNS) 的名稱。  
  
    -   對於 IBM，該值可以是任何名稱。 通常會指定「訂閱者」的網路位址。  
  
     此精靈不會驗證在此步驟中輸入的資料來源名稱和在步驟 9 中指定的認證。 為訂閱執行「散發代理程式」後，複寫才會使用它們。 透過使用用戶端工具 (如 Oracle 的 **sqlplus** ) 連接到「訂閱者」，來確定所有值都已經過測試。 如需相關資訊，請參閱 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) 及 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 在精靈的 **[訂閱者]** 頁面中，「訂閱者」即會顯示在 **[訂閱者]** 資料行中，且在 **[訂閱資料庫]** 資料行中只能讀取 **[(預設的目的地)]** ：  
  
    -   在 Oracle 中，伺服器最多只有一個資料庫，所以不需要指定資料庫。  
  
    -   對於 IBM DB2，在 DB2 連接字串的 **初始資料目錄** 屬性中指定資料庫，可在這個處理稍後描述的 **[其他連接選項]** 欄位中輸入。  
  
8.  在 **[散發代理程式安全性]** 頁面中，按一下「訂閱者」旁的屬性按鈕 (**…**)，以存取 **[散發代理程式安全性]** 對話方塊。  
  
9. 在 **[散發代理程式安全性]** 對話方塊中：  
  
    -   在 **[處理帳戶]**、 **[密碼]**及 **[確認密碼]** 欄位中，輸入「散發代理程式」應執行並與「訂閱者」建立本機連接所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶和密碼。  
  
         帳戶要求具有以下最小權限：散發資料庫中 **db_owner** 固定資料庫角色的成員；發行集存取清單 (PAL) 的成員；快照集共用的讀取權限；以及對 OLE DB 提供者之安裝目錄的讀取權限。 如需 PAL 的詳細資訊，請參閱[保護發行者](../../relational-databases/replication/security/secure-the-publisher.md)。  
  
    -   在 **[連接到訂閱者]**下的 **[登入]**、 **[密碼]**及 **[確認密碼]** 欄位中，輸入用來連接到「訂閱者」的登入和密碼。 此登入必須已經設定，還必須具有在訂閱資料庫中建立物件的足夠權限。  
  
    -   在 **[其他連接選項]** 欄位中，以連接字串形式指定「訂閱者」的任何連接選項 (Oracle 不需要其他選項)。 每個選項應以分號分隔。 以下為 DB2 連接字串的範例 (分行符號僅為便於閱讀)：  
  
        ```  
        Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
        PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
        Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
        Persist Security Info=False;Connection Pooling=True;  
        ```  
  
         字串中的大多數選項是您設定之 DB2 伺服器的專用選項，但 **將二進位當作字元處理** 選項，應一律設定為 [False] 。 需要為 **初始目錄** 選項指定值，以便識別訂閱資料庫。  
  
10. 在 **[同步排程]** 頁面中，從 **[代理程式排程]** 功能表中選取「散發代理程式」的排程 (排程通常為 **[連續執行]**)。  
  
11. 在 **[初始化訂閱]** 頁面中，指定是否應初始化訂閱以及初始化的時間 (如果是的話)：  
  
    -   只有在已建立了所有物件，並且已將全部所需資料都新增到訂閱資料庫中之後，才能清除 **[初始化]** 。  
  
    -   在 **[初始化時機]** 資料行的下拉式清單中選取 **[立即]** ，以便使「散發代理程式」在此精靈完成後將快照集檔案傳送至「訂閱者」。 選取 **[第一次同步處理時]** ，即可使代理程式在下一個執行排程傳送檔案。  
  
12. 在 **[精靈動作]** 頁面中，選擇性地編寫訂閱指令碼。 如需詳細資訊，請參閱 [Scripting Replication](../../relational-databases/replication/scripting-replication.md)。  
  
#### <a name="to-retain-tables-at-the-subscriber"></a>將資料表保留在訂閱者端  
  
-   依預設，若啟用非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者的發行集，就會將 **pre_creation_cmd** 發行項屬性的值設定為 'drop'。 這項設定會指定當複寫符合發行項中的資料表名稱時，應該要卸除「訂閱者」端的資料表。 如果您在訂閱者端有想要保留的現有資料表，請針對每一個發行項使用 [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 預存程序，並為 **pre_creation_cmd**指定 'none' 值。 `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`。  
  
#### <a name="to-generate-a-snapshot-for-the-publication"></a>產生發行集的快照集  
  
1.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
2.  以滑鼠右鍵按一下發行集，然後再按一下 **[檢視快照集代理程式的狀態]**。  
  
3.  在 [檢視快照集代理程式的狀態 - \<發行集>] 對話方塊中，按一下 [啟動]。  
  
 「快照集代理程式」完成產生快照集後，會顯示一個訊息，例如「[100%] 已產生了 17 個發行項的快照集」。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序，以程式設計的方式建立非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者的發送訂閱。  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
#### <a name="to-create-a-push-subscription-for-a-transactional-or-snapshot-publication-to-a-non-sql-server-subscriber"></a>針對非 SQL Server 訂閱者的交易式或快照式發行集建立發送訂閱  
  
1.  同時在發行者和散發者上針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者安裝最近的 OLE DB 提供者。 如需 OLE DB 提供者的複寫需求，請參閱＜ [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)＞、＜ [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)＞、＜ [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)＞。  
  
2.  在發行集資料庫的發行者端，藉由執行 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) 來確認發行集支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。  
  
    -   如果 **enabled_for_het_sub** 的值為 1，表示支援非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。  
  
    -   如果 **enabled_for_het_sub** 的值為 0，請執行 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)，並針對 **@property** 指定 **enabled_for_het_sub**，以及針對 **@value** 指定 **true**。  
  
        > [!NOTE]  
        >  在將 **enabled_for_het_sub** 變更為 **true**之前，您必須先卸除此發行集的任何現有訂閱。 當此發行集同時支援更新訂閱時，您無法將 **enabled_for_het_sub** 設定為 **true** 。 變更 **enabled_for_het_sub** 會影響其他發行集屬性。 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。  
  
3.  在發行集資料庫的發行者端，執行 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定 **@publication**、 **@subscriber**、 **[訂閱資料庫]** @property **@destination_db**、 **@subscription_type** @property **@subscription_type**值，以及 **@subscriber_type** (指定 OLE DB 提供者) 的值 3。  
  
4.  在發行集資料庫的發行者端，執行 [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)。 指定下列項目：  
  
    -   **@subscriber** 和 **@publication** 參數。  
  
    -   (選擇性) **[訂閱資料庫]** @property **@subscriber_db**、  
  
    -   針對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] @subscriber_provider **@subscriber_provider**、 **@subscriber_datasrc**、 **@subscriber_location**、 **@subscriber_provider_string**及 **@subscriber_catalog**中針對非 SQL Server 訂閱者建立訂閱。  
  
    -   將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認證，「散發者」上的「散發代理程式」執行時會針對 **@job_login** ，並將 **@job_password**＞。  
  
        > [!NOTE]  
        >  使用「Windows 整合式驗證」建立的連接一律使用由 **@job_login** 及 **@job_password**中針對非 SQL Server 訂閱者建立訂閱。 散發代理程式一律使用「Windows 整合式驗證」建立與散發者的本機連接。 依預設，代理程式會使用「Windows 整合式驗證」連接到訂閱者。  
  
    -   (選擇性) **@subscriber_security_mode** @property **@subscriber_security_mode** ，以及 **@subscriber_login** 及 **@subscriber_password**中針對非 SQL Server 訂閱者建立訂閱。  
  
    -   此訂閱之散發代理程式作業的排程。 如需詳細資訊，請參閱 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  利用遠端「散發者」來建立「發行者」上的發送訂閱時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字格式傳給「散發者」。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
## <a name="see-also"></a>另請參閱  
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)   
 [其他非 SQL Server 訂閱者](../../relational-databases/replication/non-sql/other-non-sql-server-subscribers.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
