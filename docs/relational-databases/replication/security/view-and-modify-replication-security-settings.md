---
title: 檢視及修改複寫安全性設定 | Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying replication security settings
- replication [SQL Server], security
- security [SQL Server replication], viewing settings
- viewing replication security settings
- security [SQL Server replication], modifying settings
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: f74883ab152ca1552d1193f204fc0af3a72cdb8f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287225"
---
# <a name="view-and-modify-replication-security-settings"></a>檢視及修改複寫安全性設定
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中檢視及修改複寫安全性設定。 例如，您可能要將「記錄讀取器代理程式」到「發行者」的連接從 SQL Server 驗證變更為 Windows 整合式驗證，或者在 Windows 帳戶密碼變更後，可能需要變更用來執行代理程式作業的認證。 如需有關各代理程式需要的權限資訊，請參閱＜ [複寫代理程式安全性模型](../../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要檢視及修改複寫安全性設定，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
-   **後續操作：** [修改複寫安全性設定之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您所使用的預存程序，將取決於代理程式的類型和伺服器連接的類型而定。  
  
-   您所使用的 RMO 類別和屬性，將取決於代理程式的類型和伺服器連接的類型而定。  
  
###  <a name="Security"></a> Security  
 基於安全性理由，密碼的實際值在複寫預存程序所傳回的結果集中會有遮罩。  
  
####  <a name="Permissions"></a> 權限  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 檢視並修改下列對話方塊中的安全性設定：  
  
1.  **[更新複寫密碼]** 對話方塊，可從 **的** [複寫] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]資料夾開啟。 如果變更複寫拓撲中伺服器上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶或 Windows 帳戶的密碼，請使用此對話方塊，而非更新使用該帳戶之每個代理程式的密碼。 如果多個伺服器上的代理程式使用同一個帳戶，則必須連接到每個伺服器並變更密碼。 密碼在複寫使用密碼的所有位置更新。 而並不會在其他位置更新，例如連結的伺服器。  
  
2.  [發行集屬性 - \<發行集>]  對話方塊的 [代理程式安全性]  頁面。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
3.  [訂閱屬性 - \<訂閱>]  對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ＞與＜ [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)＞。  
  
4.  [散發者屬性 - \<散發者>]  和 [散發資料庫屬性 - \<資料庫>]  對話方塊。 如需存取這些對話方塊的詳細資訊，請參閱＜ [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)＞。  
  
5.  [發行者屬性 - \<發行者>]  對話方塊。 如需存取此對話方塊的詳細資訊，請參閱＜ [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)＞。  

#### <a name="to-change-the-password-for-an-account-used-by-one-or-more-agents"></a>若要變更一個或多個代理程式使用的帳戶之密碼  
  
1.  如果該帳戶是 SQL Server 帳戶，則此對話方塊要變更 SQL Server 帳戶的密碼。 如果該帳戶是 Windows 帳戶，則應先變更 Windows 中的密碼。 如需詳細資訊，請參閱 Windows 文件集。  
  
    > [!NOTE]  
    >  在變更複寫密碼之後，必須停止並重新啟動使用該代理程式變更生效前所用密碼的每一個代理程式。  
  
2.  連接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的伺服器，然後展開伺服器節點。  
  
3.  以滑鼠右鍵按一下 **[複寫]** 資料夾，然後按一下 **[更新複寫密碼]** 。  
  
4.  在 **[更新複寫密碼]** 對話方塊中，指定帳戶與新密碼。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>變更快照集代理程式的安全性設定  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [代理程式安全性]  頁面上，按一下 [快照集代理程式]  文字方塊旁的 [安全性設定]  按鈕。  
  
2.  在 **[快照集代理程式安全性]** 對話方塊中，指定代理程式執行時所使用的帳戶：  
  
    -   在 **[代理程式帳戶]** 文字方塊中輸入新的 Windows 帳戶。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
3.  指定代理程式要從散發者連接到發行者的內容。 若您選取 **[使用下列的 SQL Server 登入]** ，必須同時指定登入：  
  
    -   在 **[登入]** 文字方塊中輸入登入。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
    > [!NOTE]  
    >  若發行者是 Oracle 發行者，則連接內容指定於 [散發者屬性 - \<散發者>]  對話方塊中。 請參閱下面用於變更內容的程序。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>變更記錄讀取器代理程式的安全性設定  
  
1.  在 [發行集屬性 - \<發行集>]  對話方塊的 [代理程式安全性]  頁面上，按一下 [記錄讀取器代理程式]  文字方塊旁的 [安全性設定]  按鈕。  
  
2.  在 **[記錄讀取器代理程式安全性]** 對話方塊中，指定代理程式執行時所使用的帳戶：  
  
    -   在 **[代理程式帳戶]** 文字方塊中輸入新的 Windows 帳戶。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
3.  指定代理程式要從散發者連接到發行者的內容。 若您選取 **[使用下列的 SQL Server 登入]** ，必須同時指定登入：  
  
    -   在 **[登入]** 文字方塊中輸入登入。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
    > [!NOTE]  
    >  若發行者是 Oracle 發行者，則連接內容指定於 [散發者屬性 - \<散發者>]  對話方塊中。 使用下一個程序變更內容。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每個已發行的資料庫都有一個「記錄讀取器代理程式」。 在一個發行集上變更代理程式的安全性設定會影響該發行集資料庫中所有發行集的設定。  
  
#### <a name="to-change-the-context-under-which-the-snapshot-agent-and-log-reader-agent-for-an-oracle-publication-make-connections-to-the-publisher"></a>若要變更 Oracle 發行集的快照集代理程式與記錄讀取器代理程式連接到發行者所使用的內容  
  
1.  在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，按一下發行者旁的屬性按鈕 ( **...** )。  
  
2.  在 **[代理程式至發行者的連接]** 區段，指定您設定的複寫管理使用者結構描述所使用之登入與密碼。 如需詳細資訊，請參閱[設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>變更發送訂閱之散發代理程式的安全性設定  
  
1.  在發行者端的 [訂閱屬性 - \<訂閱>]  對話方塊中，可做下列變更：  
  
    -   若要變更散發代理程式執行和連接到散發者時所使用的帳戶，請按一下 [代理程式處理帳戶]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[散發代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
    -   若要變更散發代理程式連接到訂閱者所使用的內容，請按一下 [訂閱者連接]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
         若您使用佇列更新訂閱，佇列讀取器代理程式亦使用此處指定的內容，連接到訂閱者。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>變更提取訂閱之散發代理程式的安全性設定  
  
1.  在訂閱者端的 [訂閱屬性 - \<訂閱>]  對話方塊中，可做下列變更：  
  
    -   若要變更散發代理程式執行和連接到訂閱者時所使用的帳戶，請按一下 [代理程式處理帳戶]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[散發代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
         若您使用佇列更新訂閱，佇列讀取器代理程式亦使用此處指定的內容，連接到訂閱者。  
  
    -   若要變更散發代理程式連接到散發者所使用的內容，請按一下 [散發者連接]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>變更發送訂閱之合併代理程式的安全性設定  
  
1.  在發行者端的 [訂閱屬性 - \<訂閱>]  對話方塊中，可做下列變更：  
  
    -   若要變更合併代理程式執行和連接到發行者與散發者時所使用的帳戶，請按一下 [代理程式處理帳戶]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[合併代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
    -   若要變更合併代理程式連接到訂閱者所使用的內容，請按一下 [訂閱者連接]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>變更提取訂閱之合併代理程式的安全性設定  
  
1.  在訂閱者端的 [訂閱屬性 - \<訂閱>]  對話方塊中，可做下列變更：  
  
    -   若要變更合併代理程式執行和連接到訂閱者時所使用的帳戶，請按一下 [代理程式處理帳戶]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[合併代理程式安全性]** 對話方塊中指定帳戶和密碼。  
  
    -   若要變更合併代理程式連接到發行者與散發者所使用的內容，請按一下 [發行者連接]  資料列，然後按一下資料列中的屬性 ( **...** ) 按鈕。 在 **[輸入連接資訊]** 對話方塊中指定內容。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-the-account-under-which-the-queue-reader-agent-runs"></a>若要變更佇列讀取器代理程式執行時所使用的帳戶  
  
1.  在 [散發者屬性 - \<散發者>]  對話方塊的 [一般]  頁面上，按一下散發資料庫旁的屬性 ( **...** ) 按鈕。  
  
2.  在 [散發資料庫屬性 - \<資料庫>]  對話方塊中，按一下 [代理程式處理帳戶]  文字方塊旁的 [安全性設定]  按鈕。  
  
3.  在 **[佇列讀取器代理程式安全性]** 對話方塊中，指定代理程式執行和連接到「散發者」時所使用的帳戶：  
  
    -   在 **[處理帳戶]** 文字方塊中輸入新的 Windows 帳戶。  
  
    -   在 **[密碼]** 和 **[確認密碼]** 文字方塊中輸入新的增強式密碼。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每個散發資料庫都會有一個佇列讀取器代理程式。 變更此代理程式的安全性設定時，會影響使用此散發資料庫之所有發行者上的所有發行集設定。  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-publisher"></a>若要變更佇列讀取器代理程式連接到發行者所使用的內容  
  
1.  在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，按一下發行者旁的屬性按鈕 ( **...** )。  
  
2.  在 **[代理程式至發行者的連接 ]** 區段，指定 **[代理程式連接模式]** 選項中 **[模擬代理程式處理帳戶]** 或 **[SQL Server 驗證]** 的值。 如果指定 **[SQL Server 驗證]** ，還要輸入 **[登入]** 與 **[密碼]** 的值。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每個散發資料庫都會有一個佇列讀取器代理程式。 變更此代理程式的安全性設定時，會影響使用此散發資料庫之所有發行者上的所有發行集設定。  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-subscriber"></a>若要變更佇列讀取器代理程式連接到訂閱者所使用的內容  
  
-   「佇列讀取器代理程式」使用與「散發代理程式」相同的連接內容進行訂閱。 如需詳細資訊，請參閱「散發代理程式」的上述程序。  
  
#### <a name="to-change-security-settings-for-an-immediate-updating-pull-subscription"></a>若要變更立即更新提取訂閱的安全性設定  
  
1.  在訂閱者端的 [訂用帳戶屬性 - \<訂用帳戶>]  對話方塊中，按一下 [發行者連線]  資料列，然後按一下資料列中的屬性 ( **&#x2026;** ) 按鈕。  
  
2.  在 **[輸入連接資訊]** 對話方塊中，選取下列其中一個選項：  
  
    -   **[使用連結伺服器或遠端伺服器的登入]** 。 若您已透過 [sp_addserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)、[sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或其他方法定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。  
  
    -   **[利用下列登入和密碼來使用 SQL Server 驗證]** 。 若您已透過尚未定義遠端伺服器或訂閱者與發行者之間連結的伺服器，請選取此選項。 複寫將為您建立連結的伺服器。 您必須指定已存在於發行者的帳戶。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  此程序會變更複寫觸發程序在「訂閱者」端發生變更時，用來從「訂閱者」連接到「發行者」的方法。 您也可以變更立即更新訂閱之與「散發代理程式」相關的設定。 如需詳細資訊，請參閱本主題前文中的程序。  
>   
>  此程序僅適用於提取訂閱。 對於發送訂閱，請使用 [sp_link_publication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 預存程序。  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>變更從發行者到散發者之管理連接的密碼  
  
1.  在 [散發者屬性 - \<散發者>]  對話方塊的 [發行者]  頁面上，於 [密碼]  與 [確認密碼]  文字方塊中輸入強式密碼。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  在 [發行者屬性 - \<發行者>]  對話方塊的 [一般]  頁面上，於 [密碼]  與 [確認密碼]  文字方塊中輸入強式密碼。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
> [!IMPORTANT]  
>  在下列所有的程序中，會在可能的情況下，於執行階段提示使用者輸入安全性認證。 如果您將認證儲存在指令碼檔案中，必須保護該檔案免於未經授權的存取。  
  
#### <a name="to-change-all-instances-of-a-stored-password-at-a-replication-server"></a>變更複寫伺服器上儲存的所有密碼執行個體  
  
1.  在 master 資料庫複寫拓撲中的伺服器上，執行 [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md)。 針對 `@login` 指定正在變更密碼的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帳戶或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入，並針對 `@password` 指定此帳戶或登入的新密碼。 這樣會變更當連接到拓撲中的其他伺服器時，由此伺服器上的所有代理程式所使用的每一個密碼執行個體。  
  
    > [!NOTE]  
    >  若只要針對拓撲中特定伺服器的連接 (如散發者或訂閱者) 變更登入和密碼，請針對 `@server` 指定此伺服器的名稱。  
  
2.  在必須更新密碼的複寫拓撲中，於每一部伺服器上重複步驟 1。  
  
    > [!NOTE]  
    >  在變更複寫密碼之後，必須停止並重新啟動使用該代理程式變更生效前所用密碼的每一個代理程式。  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>變更快照集代理程式的安全性設定  
  
1.  在發行者上，執行 [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md)，並指定 `@publication`。 這樣會傳回快照集代理程式目前的安全性設定。  
  
2.  在發行者上，執行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)，並指定 `@publication` 以及下列要變更的其中一或多個安全性設定：  
  
    -   若要變更代理程式執行時所用的 Windows 帳戶，或只要變更此帳戶的密碼，請指定 `@job_login` 和 `@job_password`。  
  
    -   若要變更連接到發行者時所用的安全性模式，請針對 `@publisher_security_mode` 指定 **1** 或 **0** 的值。  
  
    -   將連接到發行者時所用的安全性模式從 **1** 變更為 **0** 或是變更用於此連接的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入時，請指定 `@publisher_login` 和 `@publisher_password`。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>變更記錄讀取器代理程式的安全性設定  
  
1.  在發行者上，執行 [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)，並指定 `@publisher`。 這樣會傳回記錄讀取器代理程式目前的安全性設定。  
  
2.  在發行者上，執行 [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)，並指定 `@publication` 以及下列要變更的其中一或多個安全性設定：  
  
    -   若要變更代理程式執行時所用的 Windows 帳戶，或只要變更此帳戶的密碼，請指定 `@job_login` 和 `@job_password`。  
  
    -   若要變更連接到發行者時所用的安全性模式，請針對 `@publisher_security_mode` 指定 **1** 或 **0** 的值。  
  
    -   將連接到發行者時所用的安全性模式從 **1** 變更為 **0** 或是變更用於此連接的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入時，請指定 `@publisher_login` 和 `@publisher_password`。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>變更發送訂閱之散發代理程式的安全性設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)，並指定 `@publication` 和 `@subscriber`。 這樣會傳回訂閱屬性，包括在散發者上執行之散發代理程式的安全性設定。  
  
2.  在發行集資料庫的發行者上，執行 [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)，並指定 `@publication`、`@subscriber`、`@subscriber_db**`，針對 `@article` 指定 `all` 值、針對 `@property` 指定安全屬性的名稱，以及針對 `@value` 指定此屬性的新值。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   若要變更代理程式執行時所用的 Windows 帳戶，或只要變更此帳戶的密碼，請針對 `@property` 指定 **distrib_job_password** 的值，並針對 `@value` 指定新的密碼。 當變更此帳戶本身時，請重複步驟 2，針對 `@property` 指定 **distrib_job_login** 的值，並針對 `@value` 指定新的 Windows 帳戶。  
  
    -   若要變更在連接到訂閱者時所用的安全性模式，請針對 `@property` 指定 **subscriber_security_mode** 的值，並針對 `@value` 指定 **1** (Windows 整合式驗證) 或 **0** (SQL Server 驗證)。  
  
    -   將訂閱者所用的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證的登入資訊時，請針對 `@property` 指定 **subscriber_password** 的值，並針對 `@value` 指定新的密碼。 重複步驟 2，針對 `@property` 指定 **subscriber_login** 的值，並針對 `@value` 指定新的登入。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有屬性的值 (包括 **distrib_job_login** 和 **distrib_job_password**) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>變更提取訂閱之散發代理程式的安全性設定  
  
1.  在訂閱者上，執行 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)，並指定 `@publication`。 這樣會傳回訂閱屬性，包括在訂閱者上執行之散發代理程式的安全性設定。  
  
2.  在訂閱資料庫的訂閱者上，執行 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)，指定 `@publisher`、`@publisher_db`、`@publication`，並針對 `@property` 指定安全性屬性的名稱，以及針對 `@value` 指定此屬性的新值。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   若要變更代理程式執行時所用的 Windows 帳戶，或只要變更此帳戶的密碼，請針對 `@property` 指定 **distrib_job_password** 的值，並針對 `@value` 指定新的密碼。 當變更此帳戶本身時，請重複步驟 2，針對 `@property` 指定 **distrib_job_login** 的值，並針對 `@value` 指定新的 Windows 帳戶。  
  
    -   若要變更在連接到散發者時所用的安全性模式，請針對 `@property` 指定 **distributor_security_mode** 的值，並針對 `@value` 指定 **1** (Windows 整合式驗證) 或 **0** (SQL Server 驗證) 的值。  
  
    -   將散發者所用的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證的登入資訊時，請針對 `@property` 指定 **distributor_password** 的值，並針對 `@value` 指定新的密碼。 重複步驟 2，針對 `@property` 指定 **distributor_login** 的值，並針對 `@value` 指定新的登入。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>變更發送訂閱之合併代理程式的安全性設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)，並指定 `@publication`、`@subscriber,` 及 `@subscriber_db`。 這樣會傳回訂閱屬性，包括在散發者上執行之合併代理程式的安全性設定。  
  
2.  在發行集資料庫的發行者上，執行 [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)，並指定 `@publication`、`@subscriber`、`@subscriber_db`，針對 `@property` 指定安全性屬性的名稱，以及針對 `@value` 指定此屬性的新值。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   若要變更代理程式執行時所用的 Windows 帳戶，或只要變更此帳戶的密碼，請針對 `@property` 指定 **merge_job_password** 的值，並針對 `@value` 指定新的密碼。 當變更此帳戶本身時，請重複步驟 2，針對 `@property` 指定**merge_job_login** 的值，並針對 `@value` 指定新的 Windows 帳戶。  
  
    -   若要變更在連接到訂閱者時所用的安全性模式，請針對 `@property` 指定 **subscriber_security_mode** 的值，並針對 `@value` 指定 **1** (Windows 整合式驗證) 或 **0** (SQL Server 驗證)。  
  
    -   將訂閱者所用的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證的登入資訊時，請針對 `@property` 指定 **subscriber_password** 的值，並針對 `@value` 指定新的密碼。 重複步驟 2，針對 `@property` 指定 **subscriber_login** 的值，並針對 `@value` 指定新的登入。  
  
    -   若要變更在連接到發行者時所用的安全性模式，請針對 `@property` 指定 **publisher_security_mode** 的值，並針對 `@value` 指定 **1** (Windows 整合式驗證) 或**0** (SQL Server 驗證) 的值。  
  
    -   將發行者所用的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證的登入資訊時，請針對 `@property` 指定 **publisher_password** 的值，並針對 `@value` 指定新的密碼。 重複步驟 2，針對 `@property` 指定 **publisher_login** 的值，並針對 `@value` 指定新的登入。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有屬性的值 (包括 **merge_job_login** 和 **merge_job_password**) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>變更提取訂閱之合併代理程式的安全性設定  
  
1.  在訂閱者上，執行 [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)，並指定 ``@publication``。 這樣會傳回訂閱屬性，包括在訂閱者上執行之合併代理程式的安全性設定。  
  
2.  在訂閱資料庫的訂閱者上，執行 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)，指定 `@publisher`、`@publisher_db`、`@publication`，並針對 `@property` 指定安全性屬性的名稱，以及針對 `@value` 指定此屬性的新值。  
  
3.  針對以下變更的每一個安全性屬性重複步驟 2：  
  
    -   若要變更代理程式執行時所用的 Windows 帳戶，或只要變更此帳戶的密碼，請針對 `@property` 指定 **merge_job_password** 的值，並針對 `@value` 指定新的密碼。 當變更此帳戶本身時，請重複步驟 2，針對 `@property` 指定**merge_job_login** 的值，並針對 `@value` 指定新的 Windows 帳戶。  
  
    -   若要變更在連接到散發者時所用的安全性模式，請針對 `@property` 指定 **distributor_security_mode** 的值，並針對 `@value` 指定 **1** (Windows 整合式驗證) 或 **0** (SQL Server 驗證) 的值。  
  
    -   將散發者所用的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證的登入資訊時，請針對 `@property` 指定 **distributor_password** 的值，並針對 `@value` 指定新的密碼。 重複步驟 2，針對 `@property` 指定 **distributor_login** 的值，並針對 `@value` 指定新的登入。  
  
    -   若要變更在連接到發行者時所用的安全性模式，請針對 `@property` 指定 **publisher_security_mode** 的值，並針對 `@value` 指定 **1** (Windows 整合式驗證) 或**0** (SQL Server 驗證) 的值。  
  
    -   將發行者所用的安全性模式變更為 SQL Server 驗證，或變更 SQL Server 驗證的登入資訊時，請針對 `@property` 指定 **publisher_password** 的值，並針對 `@value` 指定新的密碼。 重複步驟 2，針對 `@property` 指定 **publisher_login** 的值，並針對 `@value` 指定新的登入。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent-to-generate-a-filtered-snapshot-for-a-subscriber"></a>變更快照集代理程式的安全性設定，為訂閱者產生篩選過的快照集  
  
1.  在發行者上，執行 [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md)，並指定 `@publication`。 在結果集中，注意訂閱者要變更之資料分割的 **job_name** 值。  
  
2.  在發行者上，執行 [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md) 並指定 `@publication`、針對 `dynamic_snapshot_jobname` 指定從步驟 1 中取得的值、針對 `@job_password` 指定新的密碼，或針對 `@job_login` 和 `@job_password` 指定此代理程式所用 Windows 帳戶的登入和密碼。  
  
    > [!IMPORTANT]  
    >  當利用遠端散發者來設定發行者時，提供給所有參數的值 (包括 *job_login* 和 *job_password*) 都會以純文字的方式傳給散發者。 您應該先加密「發行者」及其遠端「散發者」之間的連接，再執行這個預存程序。 如需詳細資訊，請參閱[啟用 Database Engine 的加密連接 &#40;SQL Server 組態管理員&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-change-security-settings-for-the-queue-reader-agent"></a>變更佇列讀取器代理程式的安全性設定  
  
1.  在散發者上，執行 [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)。 這樣會傳回佇列讀取器代理程式執行時所用的目前 Windows 帳戶。  
  
    -   在散發者上，執行 [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)，並針對 `@job_login` 和 `@job_password` 指定 Windows 帳戶設定。  
  
    > [!NOTE]  
    >  變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。 每個散發資料庫都會有一個佇列讀取器代理程式。 變更此代理程式的安全性設定時，會影響使用此散發資料庫之所有發行者上的所有發行集設定。  
  
2.  佇列讀取器代理程式會使用與訂閱之散發代理程式相同的連接內容連接到訂閱者。  
  
#### <a name="to-change-security-mode-used-by-an-immediate-updating-subscriber-when-connecting-to-the-publisher"></a>變更立即更新訂閱者連接到發行者時所用的安全性模式  
  
1.  在訂閱資料庫的訂閱者上，執行 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。 指定 `@publisher`、 `@publication`、 `@publisher_db`的發行集資料庫名稱，和 `@security_mode`的下列其中一個值：  
  
    -   **0** - 在發行者上進行更新時使用「SQL Server 驗證」。 此選項要求您在發行者上針對 `@login` 和 `@password`指定有效的登入。  
  
    -   **1** - 在連接到發行者時，使用在訂閱者上進行變更之使用者的安全性內容。 如需與此安全性模式有關的限制，請參閱 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 。  
  
    -   **2** - 使用透過 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 所建立之現有使用者定義的連結伺服器登入。  
  
#### <a name="to-change-the-password-for-a-remote-distributor"></a>變更遠端散發者的密碼  
  
1.  在散發資料庫的散發者上執行 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md)，針對 `@password` 指定此登入的新密碼。  
  
    > [!IMPORTANT]  
    >  請勿直接變更 **distributor_admin** 的密碼。  
  
2.  在使用此遠端散發者的每一個發行者上，執行 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md)，並針對 `@password` 指定步驟 1 的密碼。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
  
> [!IMPORTANT]  
>  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) 密碼編譯服務 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 。  
  
#### <a name="to-change-all-instances-of-a-password-stored-on-a-replication-server"></a>變更複寫伺服器上儲存的所有密碼執行個體  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與複寫伺服器的連接。  
  
2.  使用步驟 1 中的連接建立 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 類別的執行個體。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> 方法。 指定下列參數：  
  
    -   *security_mode* - <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> 值，可指定變更所有密碼執行個體所針對的驗證類型。  
  
    -   *login* - 變更所有密碼執行個體所針對的登入。  
  
    -   *password* - 新的密碼值。  
  
        > [!IMPORTANT]  
        >  可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須儲存認證，請使用 Windows .NET Framework 提供的 [密碼編譯服務](https://go.microsoft.com/fwlink/?LinkId=34733) 。  
  
        > [!NOTE]  
        >  只有 **sysadmin** 固定伺服器角色的成員，才能呼叫這個方法。  
  
4.  在必須更新密碼的複寫拓撲中，於每一部伺服器上重複步驟 1-3。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription-to-a-transactional-publication"></a>針對交易式發行集的發送訂閱變更散發代理程式的安全性設定  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransSubscription> 類別的執行個體。  
  
3.  針對訂閱設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 屬性，並針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  在 <xref:Microsoft.SqlServer.Replication.TransSubscription>的執行個體上設定以下其中一個或多個安全性屬性：  
  
    -   若要變更代理程式執行所使用之 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>欄位。  
  
    -   若要指定「Windows 整合式驗證」當做代理程式連接到訂閱者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 欄位設定為 **true**＞。  
  
    -   若要指定「SQL Server 驗證」當做代理程式連接到訂閱者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 欄位設定為 **false**，並針對 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> ＞與＜ <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位指定訂閱者登入認證。  
  
        > [!NOTE]  
        >  與散發者的代理程式連接一律使用 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>指定的 Windows 認證來建立。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  (選擇性) 如果您已針對 **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>的值，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您已針對 **false** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 的值 (預設值)，則會立即將變更傳送到伺服器。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription-to-a-transactional-publication"></a>針對交易式發行集的提取訂閱變更散發代理程式的安全性設定  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 類別的執行個體。  
  
3.  針對訂閱設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性，並針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  在 <xref:Microsoft.SqlServer.Replication.TransPullSubscription>的執行個體上設定以下其中一個或多個安全性屬性：  
  
    -   若要變更代理程式執行所使用之 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>欄位。  
  
    -   若要指定「Windows 整合式驗證」當做代理程式連接到散發者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 欄位設定為 **true**＞。  
  
    -   若要指定「SQL Server 驗證」當做代理程式連接到散發者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 欄位設定為 **false**，並針對 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> ＞與＜ <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位指定訂閱者登入認證。  
  
        > [!NOTE]  
        >  與訂閱者的代理程式連接一律使用 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>指定的 Windows 認證來建立。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  (選擇性) 如果您已針對 **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>的值，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您已針對 **false** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 的值 (預設值)，則會立即將變更傳送到伺服器。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription-to-a-merge-publication"></a>針對合併式發行集的提取訂閱變更合併代理程式的安全性設定  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 類別的執行個體。  
  
3.  針對訂閱設定 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 屬性，並針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  在 <xref:Microsoft.SqlServer.Replication.MergePullSubscription>的執行個體上設定以下其中一個或多個安全性屬性：  
  
    -   若要變更代理程式執行所使用之 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>欄位。  
  
    -   若要指定「Windows 整合式驗證」當做代理程式連接到散發者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 欄位設定為 **true**＞。  
  
    -   若要指定「SQL Server 驗證」當做代理程式連接到散發者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 欄位設定為 **false**，並針對 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> ＞與＜ <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位指定訂閱者登入認證。  
  
    -   若要指定「Windows 整合式驗證」當做代理程式連接到發行者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 欄位設定為 **true**＞。  
  
    -   若要指定「SQL Server 驗證」當做代理程式連接到發行者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 欄位設定為 **false**，並針對 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> ＞與＜ <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位指定訂閱者登入認證。  
  
        > [!NOTE]  
        >  與訂閱者的代理程式連接一律使用 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>指定的 Windows 認證來建立。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  (選擇性) 如果您已針對 **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>的值，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您已針對 **false** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 的值 (預設值)，則會立即將變更傳送到伺服器。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription-to-a-merge-publication"></a>針對合併式發行集的發送訂閱變更合併代理程式的安全性設定  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 類別的執行個體。  
  
3.  針對訂閱設定 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 屬性，並針對 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定步驟 1 中的連接。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 3 中的訂閱屬性定義不正確，或者此訂閱不存在。  
  
5.  在 <xref:Microsoft.SqlServer.Replication.MergeSubscription>的執行個體上設定以下其中一個或多個安全性屬性：  
  
    -   若要變更代理程式執行所使用之 Windows 帳戶的認證，請設定 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>欄位。  
  
    -   若要指定「Windows 整合式驗證」當做代理程式連接到訂閱者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 欄位設定為 **true**＞。  
  
    -   若要指定「SQL Server 驗證」當做代理程式連接到訂閱者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 欄位設定為 **false**，並針對 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> ＞與＜ <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 欄位指定訂閱者登入認證。  
  
    -   若要指定「Windows 整合式驗證」當做代理程式連接到發行者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 欄位設定為 **true**＞。  
  
    -   若要指定「SQL Server 驗證」當做代理程式連接到發行者時所使用的驗證類型，請將 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 屬性的 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 欄位設定為 **false**，並針對 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> ＞與＜ <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> 欄位指定訂閱者登入認證。  
  
        > [!NOTE]  
        >  與散發者的代理程式連接一律使用 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>指定的 Windows 認證來建立。 透過 Windows 驗證進行遠端連接時，也會使用這個帳戶。  
  
6.  (選擇性) 如果您已針對 **P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>的值，請呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法來認可伺服器上的變更。 如果您已針對 **false** 指定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 的值 (預設值)，則會立即將變更傳送到伺服器。  
  
#### <a name="to-change-the-login-information-used-by-an-immediate-updating-subscriber-when-it-connects-to-the-transactional-publisher"></a>變更立即更新訂閱者連接到交易式發行者時所用的登入資訊  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與「訂閱者」的連接。  
  
2.  為訂閱資料庫建立 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 類別的執行個體。 指定 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> 並針對 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 指定步驟 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的屬性。 如果此方法傳回 **false**，則表示步驟 2 中的資料庫屬性定義不正確，或者此訂閱資料庫不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> 方法，傳遞以下參數：  
  
    -   *Publisher* - 發行者的名稱。  
  
    -   *PublisherDB* - 發行集資料庫的名稱。  
  
    -   *Publication* - 立即更新訂閱者訂閱的發行集名稱。  
  
    -   *Distributor* - 散發者的名稱。  
  
    -   *PublisherSecurity* - A <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> 物件，可在連接到發行者和連接的登入認證時，指定立即更新訂閱者所使用之安全性模式的類型。  
  
###  <a name="PShellExample"></a> 範例 (RMO)  
 這個範例會檢查提供的登入值，並針對提供的 Windows 登入或 SQL Server 登入 (在伺服器上由複寫儲存) 變更其所有密碼。  
  
 [!code-cs[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> 後續操作：修改複寫安全性設定之後  
 變更代理程式的登入或密碼之後，您必須先停止並重新啟動代理程式，變更才會生效。  
  
## <a name="see-also"></a>另請參閱  
 [Replication Management Objects Concepts](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [升級複寫指令碼 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [用於複寫的身分識別和存取控制](../../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [複寫代理程式安全性模型](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [檢視及修改複寫安全性設定](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  
