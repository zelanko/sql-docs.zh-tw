---
title: 管理識別欄位 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b9a7b28c288ef80d24fb67479727d94c3c09fa5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060524"
---
# <a name="manage-identity-columns"></a>管理識別欄位
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中管理識別欄位。 當訂閱者插入複寫回發行者時，必須管理識別欄位，以免在訂閱者和發行者上指派相同的識別值。 複寫可以自動管理識別範圍，或者您可以選擇手動處理識別範圍管理。  如需複寫提供之識別範圍管理選項的詳細資訊，請參閱[複寫識別欄位](replicate-identity-columns.md)。  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   在一個以上發行集中發行資料表時，您必須針對兩個發行集指定相同的識別範圍管理選項。 如需詳細資訊，請參閱[發行資料和資料庫物件](publish-data-and-database-objects.md)中的＜在多個發行集中發行資料表＞。  
  
-   若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱 [序號](../../sequence-numbers/sequence-numbers.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在 [新增發行集嚮導] 之 [發行項**屬性- \<Article> ** ] 對話方塊的 [**屬性**] 索引標籤上，指定識別欄位管理選項。 如需使用此精靈的詳細資訊，請參閱[建立發行集](create-a-publication.md)。 在「新增發行集精靈」中：  
  
-   如果在 **[發行集類型]** 頁面中選取 **[合併式發行集]** 或 **[具更新訂閱的交易式發行集]** ，請選取自動或手動識別範圍管理 (依預設為自動，建議使用)。 發行資料表後，將無法修改其屬性，但是可以修改其他相關屬性。  
  
-   如果選取其他發行集類型，應將識別範圍管理設定為手動。  
  
 在 [發行項** \<Article> 屬性**-] 的 [**屬性**] 索引標籤上修改識別範圍和臨界值，這可在 [**發行集 \<Publication> 屬性-** ] 對話方塊中取得。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。  
  
#### <a name="to-specify-an-identity-column-management-option"></a>若要指定識別欄位管理選項  
  
1.  如果「發行者」在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]版本上執行，請在「新增發行集精靈」的 **[發行集類型]** 頁面中，選取 **[合併式發行集]** 或 **[具更新訂閱的交易式發行集]**。  
  
2.  在 **[發行項]** 頁面中，選取具有識別欄位的資料表。  
  
3.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
4.  在 [發行項**屬性- \<Article> ** ] 對話方塊的 [**屬性**] 索引標籤上，于 [**識別範圍管理**] 區段中，將 [**自動管理識別範圍**] 屬性設定為 [**自動**] 或 [**手動**] （針對執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的發行者）或 [ **True** ] 或 [ **False** ] （針對執行之前版本的發行者 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ）。  
  
5.  如果在步驟 4 中選取了 **[自動]** 或 **[True]** ，請在下表中輸入選項的值。 如需如何使用這些設定的詳細資訊，請參閱[複寫識別欄位](replicate-identity-columns.md)中的＜指派識別範圍＞一節。  
  
    |選項|值|描述|  
    |------------|-----------|-----------------|  
    |**發行者範圍大小**|範圍大小的整數值 (例如 20000)。|請參閱[複寫識別欄位](replicate-identity-columns.md)中的＜指派識別範圍＞一節。|  
    |**訂閱者範圍大小**|範圍大小的整數值 (例如 10000)。|請參閱[複寫識別欄位](replicate-identity-columns.md)中的＜指派識別範圍＞一節。|  
    |**範圍臨界值百分比**|臨界值百分比的整數值 (例如 90 相當於 90%)。|指派新的識別範圍之前，節點處所用的識別值總計百分比。<br /><br /> 注意：必須指定這個值，但只能由下列人員使用：使用佇列更新訂閱的訂閱者；以及執行 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 或其他舊版 SQL Server 之合併式發行集的訂閱者。 如需詳細資訊，請參閱[複寫識別欄位](replicate-identity-columns.md)中的＜指派識別範圍＞一節。|  
    |**[下一個範圍起始值]**|整數值。 唯讀。|下一個範圍的開始值。 例如，如果目前範圍是 5001-6000，則該值為 6001。|  
    |**[最大識別值]**|整數值。 唯讀。|識別欄位的最大值。 由資料行的基底資料型別決定。|  
    |**連續**|整數值。 唯讀。|每次插入時，應增加或是減少的識別欄位的值數量：通常設定為 1。|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-modify-identity-ranges-and-thresholds-after-a-table-is-published"></a>若要在發行資料表後修改識別範圍和臨界值  
  
1.  在 [**發行集屬性- \<Publication> ** ] 對話方塊的 [發行項] 頁面上，選取具有識別欄位的資料表。 **Articles**  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
3.  在 [發行項**屬性 \<Article> -** ] 對話方塊的 [**屬性**] 索引標籤上，于 [**識別範圍管理**] 區段中，輸入下列一個或多個屬性的值： **[發行者範圍大小]、[****訂閱者範圍大小**] 和 [**範圍臨界值百分比**]。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  在 [發行集**屬性- \<Publication> ** ] 對話方塊上，按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以在建立發行項時，使用複寫預存程序來指定識別範圍管理選項。  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>在針對交易式發行集定義發行項時，啟用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 如果所發行的來源資料表具有識別欄位，**請為** ** \@ identityrangemanagementoption**指定一個值、指派給發行者的識別值範圍** \@ Pub_identity_range**、 ** \@ identity_range**的每個訂閱者指派的識別值範圍，以及在指派新的識別範圍之前，所** \@ 使用的總**識別值百分比。 如需定義發行項的詳細資訊，請參閱[定義發行項](define-an-article.md)。  
  
    > [!NOTE]  
    >  請確定識別欄位的資料類型夠大，足以支援指派給所有訂閱者的識別總範圍。  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>在針對交易式發行集定義發行項時，停用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。 為** \@ identityrangemanagementoption**指定**manual**的值。 如需定義發行項的詳細資訊，請參閱[定義發行項](define-an-article.md)。  
  
2.  在訂閱者上指派識別發行項欄位的範圍，以免產生更新訂閱者的衝突。 如需詳細資訊，請參閱[複寫識別欄位](replicate-identity-columns.md)主題中的＜為手動識別範圍管理指派範圍＞一節。  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>在針對合併式發行集定義發行項時，啟用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 如果所發行的來源資料表具有識別欄位，**請為** ** \@ identityrangemanagementoption**指定一個值、指派給** \@ pub_identity_range**的伺服器訂閱的識別值範圍、指派給「發行者」的識別值範圍和** \@ identity_range**的每個用戶端訂閱，以及在新的識別範圍指派給「 ** \@ 閾值**」之前所使用的總識別值百分比。 如需要指派哪些新識別範圍的詳細資訊，請參閱[複寫識別欄位](replicate-identity-columns.md)主題中的＜指派識別範圍＞。 如需定義發行項的詳細資訊，請參閱[定義發行項](define-an-article.md)。  
  
    > [!NOTE]  
    >  請確定識別欄位的資料類型夠大，足以支援指派給所有訂閱者的識別總範圍，特別是具有伺服器訂閱的訂閱者  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>在針對合併式發行集定義發行項時，停用自動識別範圍管理  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)。 針對** \@ identityrangemanagementoption**指定下列其中一個值：  
  
    -   **manual** - 必須手動指派識別範圍來更新訂閱者。  
  
    -   **none** - 發行者上的識別欄位將不會定義為訂閱者上的識別欄位。  
  
     如需定義發行項的詳細資訊，請參閱[定義發行項](define-an-article.md)。  
  
2.  在訂閱者上指派識別發行項欄位的範圍，以免產生更新訂閱者的衝突。  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集中的現有發行項，變更自動識別範圍管理設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql) ，並記下結果集中 **identityrangemanagementoption** 的值。 如果此值為 **0**，不會啟用自動識別範圍管理。  
  
2.  如果結果集中 **identityrangemanagementoption** 的值為 **1**，請依照以下方式變更設定：  
  
    -   若要變更指派的識別範圍，請在發行集資料庫的發行者上，執行 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) 。 針對 [ ** \@ 屬性**] 指定 [ **identity_range** ] 或 [ **pub_identity_range** ] 值，並針對 [ ** \@ 值**] 指定新的 [範圍] 值  
  
    -   若要變更指派新範圍的臨界值，請在發行集資料庫的發行者上，執行 [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) 。 針對 [ ** \@ 屬性**] 指定 [**閾值**] 的值，並針對 [ ** \@ 值**] 指定新的臨界值。  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-merge-publication"></a>針對合併式發行集中的現有發行項，變更自動識別範圍管理設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) ，並記下結果集中 **identity_support** 的值。 如果此值為 **0**，不會啟用自動識別範圍管理。  
  
2.  如果結果集中 **identity_support** 的值為 **1**，請依照以下方式變更設定：  
  
    -   若要變更指派的識別範圍，請在發行集資料庫的發行者上，執行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) 。 針對 [ ** \@ 屬性**] 指定 [ **identity_range** ] 或 [ **pub_identity_range** ] 值，並針對 [ ** \@ 值**] 指定新的 [範圍] 值  
  
    -   若要變更指派新範圍的臨界值，請在發行集資料庫的發行者上，執行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) 。 針對 [ ** \@ 屬性**] 指定 [**閾值**] 的值，並針對 [ ** \@ 值**] 指定新的臨界值。 如需要指派哪些新識別範圍的詳細資訊，請參閱[複寫識別欄位](replicate-identity-columns.md)主題中的＜指派識別範圍＞。  
  
    -   若要停用自動識別範圍管理，請在發行集資料庫的發行者上，執行 [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) 。 針對 [ ** \@ 屬性**] 指定**identityrangemanagementoption**的值，並為 [ ** \@ 值**] 選擇 [**手動**] 或 [**無**]。  
  
## <a name="see-also"></a>另請參閱  
 [Peer-to-Peer Transactional Replication](../transactional/peer-to-peer-transactional-replication.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [複寫識別欄位](replicate-identity-columns.md)  
  
  
