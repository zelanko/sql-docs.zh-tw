---
title: 管理識別欄位 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
caps.latest.revision: 42
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8173b90d4c23ca612e80175d59969e259c2cb24c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32964683"
---
# <a name="manage-identity-columns"></a>管理識別欄位
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中管理識別欄位。 當訂閱者插入複寫回發行者時，必須管理識別欄位，以免在訂閱者和發行者上指派相同的識別值。 複寫可以自動管理識別範圍，或者您可以選擇手動處理識別範圍管理。  如需複寫提供之識別範圍管理選項的詳細資訊，請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要管理識別欄位，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   在一個以上發行集中發行資料表時，您必須針對兩個發行集指定相同的識別範圍管理選項。 如需詳細資訊，請參閱[發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)中的＜在多個發行集中發行資料表＞。  
  
-   若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱 [序號](../../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [新增發行集精靈] 的 [發行項屬性 - \<發行項>] 對話方塊的 [屬性] 索引標籤上，指定識別欄位管理選項。 如需使用此精靈的詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。 在「新增發行集精靈」中：  
  
-   如果在 **[發行集類型]** 頁面中選取 **[合併式發行集]** 或 **[具更新訂閱的交易式發行集]** ，請選取自動或手動識別範圍管理 (依預設為自動，建議使用)。 發行資料表後，將無法修改其屬性，但是可以修改其他相關屬性。  
  
-   如果選取其他發行集類型，應將識別範圍管理設定為手動。  
  
 在 [發行項屬性 - \<發行項>] 對話方塊的 [屬性] 索引標籤上修改識別範圍和臨界值，其可於 [發行集屬性 - \<發行集>] 對話方塊中提供。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
#### <a name="to-specify-an-identity-column-management-option"></a>若要指定識別欄位管理選項  
  
1.  如果「發行者」在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本上執行，請在「新增發行集精靈」的 **[發行集類型]** 頁面中，選取 **[合併式發行集]** 或 **[具更新訂閱的交易式發行集]**。  
  
2.  在 **[發行項]** 頁面中，選取具有識別欄位的資料表。  
  
3.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
4.  在 [發行項屬性 - \<發行項>] 對話方塊的 [屬性] 索引標籤上，於 [識別範圍管理] 區段中，將 [自動管理識別範圍] 屬性設定為 [自動] 或 [手動] (針對執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的發行者) 或是 [True] 或 [False] (針對執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的發行者)。  
  
5.  如果在步驟 4 中選取了 **[自動]** 或 **[True]** ，請在下表中輸入選項的值。 如需如何使用這些設定的詳細資訊，請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)中的＜指派識別範圍＞一節。  
  
    |選項|ReplTest1|描述|  
    |------------|-----------|-----------------|  
    |**發行者範圍大小**|範圍大小的整數值 (例如 20000)。|請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)中的＜指派識別範圍＞一節。|  
    |**訂閱者範圍大小**|範圍大小的整數值 (例如 10000)。|請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)中的＜指派識別範圍＞一節。|  
    |**範圍臨界值百分比**|臨界值百分比的整數值 (例如 90 相當於 90%)。|指派新的識別範圍之前，節點處所用的識別值總計百分比。<br /><br /> <br /><br /> 注意：必須指定這個值，但只能由下列人員使用：使用佇列更新訂閱的訂閱者；以及執行 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 或其他舊版 SQL Server 之合併式發行集的訂閱者。 如需詳細資訊，請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)中的＜指派識別範圍＞一節。|  
    |**[下一個範圍起始值]**|整數值。 唯讀。|下一個範圍的開始值。 例如，如果目前範圍是 5001-6000，則該值為 6001。|  
    |**[最大識別值]**|整數值。 唯讀。|識別欄位的最大值。 由資料行的基底資料型別決定。|  
    |**[遞增]**|整數值。 唯讀。|每次插入時，應增加或是減少的識別欄位的值數量：通常設定為 1。|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-modify-identity-ranges-and-thresholds-after-a-table-is-published"></a>若要在發行資料表後修改識別範圍和臨界值  
  
1.  在 [發行集屬性 - \<發行集>] 對話方塊的 [發行項] 頁面上，選取具有識別欄位的資料表。  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
3.  在 [發行項屬性 - \<發行項>] 對話方塊的 [屬性] 索引標籤上，於 [識別範圍管理] 區段中輸入下列其中一或多個屬性的值：[發行者範圍大小]、[訂閱者範圍大小] 和 [範圍臨界值百分比]。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  在 [發行集屬性 - \<發行集>] 對話方塊上，按一下 [確定]。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以在建立發行項時，使用複寫預存程序來指定識別範圍管理選項。  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>在針對交易式發行集定義發行項時，啟用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 如果發行的來源資料表有識別欄位，請針對 **@identityrangemanagementoption** 指定 **@identityrangemanagementoption**的值、針對 **@pub_identity_range**指定指派給發行者的識別值範圍、針對 **@identity_range**指定指派給每一個訂閱者的識別值範圍，以及針對 **@threshold**中管理識別欄位。 如需定義發行項的詳細資訊，請參閱[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  請確定識別欄位的資料類型夠大，足以支援指派給所有訂閱者的識別總範圍。  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>在針對交易式發行集定義發行項時，停用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 針對 **@identityrangemanagementoption** 指定 **@identityrangemanagementoption**中管理識別欄位。 如需定義發行項的詳細資訊，請參閱[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在訂閱者上指派識別發行項欄位的範圍，以免產生更新訂閱者的衝突。 如需詳細資訊，請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)主題中的＜為手動識別範圍管理指派範圍＞一節。  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>在針對合併式發行集定義發行項時，啟用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 如果發行的來源資料表有識別欄位，請針對 **@identityrangemanagementoption** 指定 **@identityrangemanagementoption**的值、針對 **@pub_identity_range**指定指派給伺服器訂閱的識別值範圍、針對 **@identity_range**指定指派給每一個訂閱者的識別值範圍，以及針對 **@threshold**中管理識別欄位。 如需要指派哪些新識別範圍的詳細資訊，請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)主題中的＜指派識別範圍＞。 如需定義發行項的詳細資訊，請參閱[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  請確定識別欄位的資料類型夠大，足以支援指派給所有訂閱者的識別總範圍，特別是具有伺服器訂閱的訂閱者  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>在針對合併式發行集定義發行項時，停用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 針對 **@identityrangemanagementoption**指定下列其中一個值：  
  
    -   **manual** - 必須手動指派識別範圍來更新訂閱者。  
  
    -   **none** - 發行者上的識別欄位將不會定義為訂閱者上的識別欄位。  
  
     如需定義發行項的詳細資訊，請參閱[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在訂閱者上指派識別發行項欄位的範圍，以免產生更新訂閱者的衝突。  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中的現有發行項，變更自動識別範圍管理設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) ，並記下結果集中 **identityrangemanagementoption** 的值。 如果此值為 **0**，不會啟用自動識別範圍管理。  
  
2.  如果結果集中 **identityrangemanagementoption** 的值為 **1**，請依照以下方式變更設定：  
  
    -   若要變更指派的識別範圍，請在發行集資料庫的發行者上，執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 。 針對 **@property** ，在 **identity_range** 指定 **@property** 的值，以及針對 **@value**中管理識別欄位。  
  
    -   若要變更指派新範圍的臨界值，請在發行集資料庫的發行者上，執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 。 針對 **@property** 指定 **@property** 的值，並針對 **@value**中管理識別欄位。  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-merge-publication"></a>針對合併式發行集中的現有發行項，變更自動識別範圍管理設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) ，並記下結果集中 **identity_support** 的值。 如果此值為 **0**，不會啟用自動識別範圍管理。  
  
2.  如果結果集中 **identity_support** 的值為 **1**，請依照以下方式變更設定：  
  
    -   若要變更指派的識別範圍，請在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 。 針對 **@property** ，在 **identity_range** 指定 **@property** 的值，以及針對 **@value**中管理識別欄位。  
  
    -   若要變更指派新範圍的臨界值，請在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 。 針對 **@property** 指定 **@property** 的值，並針對 **@value**中管理識別欄位。 如需要指派哪些新識別範圍的詳細資訊，請參閱[複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)主題中的＜指派識別範圍＞。  
  
    -   若要停用自動識別範圍管理，請在發行集資料庫的發行者上，執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 。 針對 **identityrangemanagementoption** 指定 **@property** 的值，以及針對 **@identityrangemanagementoption** ，在 **none** 指定 **@value**中管理識別欄位。  
  
## <a name="see-also"></a>另請參閱  
 [Peer-to-Peer Transactional Replication](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
