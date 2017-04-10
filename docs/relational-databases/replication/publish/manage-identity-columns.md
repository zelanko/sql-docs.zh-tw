---
title: "管理識別欄位 | Microsoft Docs"
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
  - "識別值 [SQL Server 複寫]"
  - "合併式複寫 [SQL Server 複寫], 識別範圍管理"
  - "發行 [SQL Server 複寫], 識別欄位"
  - "異動複寫, 識別範圍管理"
  - "識別欄位 [SQL Server], 複寫"
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 管理識別欄位
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中管理識別欄位。 當訂閱者插入複寫回發行者時，必須管理識別欄位，以免在訂閱者和發行者上指派相同的識別值。 複寫可以自動管理識別範圍，或者您可以選擇手動處理識別範圍管理。  複寫提供的識別範圍管理選項的相關資訊，請參閱 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要管理識別欄位，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   在一個以上發行集中發行資料表時，您必須針對兩個發行集指定相同的識別範圍管理選項。 如需詳細資訊，請參閱 」 中超過一個發行集中發行資料表 」 中 [發行資料和資料庫物件](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
-   若要建立自動遞增的數字，可以用於多個資料表中，或可呼叫的應用程式而不參考任何資料表，請參閱 [序號](../../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 指定識別欄位管理選項上 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>** 新增發行集精靈] 對話方塊。 如需使用此精靈的詳細資訊，請參閱 [建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。 在「新增發行集精靈」中：  
  
-   如果您選取 **合併式發行集** 或 **具有可更新訂閱的交易式發行集** 上 **發行集類型** 頁面上，選取 [自動或手動識別範圍管理 （自動的預設值，建議使用）。 發行資料表後，將無法修改其屬性，但是可以修改其他相關屬性。  
  
-   如果選取其他發行集類型，應將識別範圍管理設定為手動。  
  
 上修改識別範圍和臨界值 **屬性** ] 索引標籤的 **發行項屬性-\< 發行項>**, ，可用於 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
#### 若要指定識別欄位管理選項  
  
1.  如果 「 發行者 」 執行的版本 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], 上 **發行集類型** 新的發行集精靈 」，選取頁面 **合併式發行集** 或 **具有可更新訂閱的交易式發行集**。  
  
2.  在 **文章** 頁面上，選取具有識別資料行的資料表。  
  
3.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
4.  上 **屬性** ] 索引標籤 **發行項屬性-\< 發行項>** 對話方塊中，於 **識別範圍管理** 區段中，將 **自動管理識別範圍** 屬性 **自動** 或 **手動** (執行 「 發行者 」 的 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本)，或 **True** 或 **False** (執行版本的發行者 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之前 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)])。  
  
5.  如果您選取 **自動** 或 **True** 在步驟 4 中，輸入下表中的選項值。 如需有關如何使用這些設定的詳細資訊，請參閱 「 指派識別範圍 」 一節 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
    |選項|值|描述|  
    |------------|-----------|-----------------|  
    |**發行者範圍大小**|範圍大小的整數值 (例如 20000)。|請參閱 「 指派識別範圍 」 一節 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
    |**訂閱者範圍大小**|範圍大小的整數值 (例如 10000)。|請參閱 「 指派識別範圍 」 一節 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
    |**範圍臨界值百分比**|臨界值百分比的整數值 (例如 90 相當於 90%)。|指派新的識別範圍之前，節點處所用的識別值總計百分比。<br /><br /> <br /><br /> 注意︰ 必須指定此值，但它只能由: 「 訂閱者 」 使用佇列更新訂閱。與訂閱者合併式發行集執行 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 或舊版的其他 SQL Server 版本。 如需詳細資訊，請參閱 「 指派識別範圍 」 一節 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
    |**[下一個範圍起始值]**|整數值。 唯讀。|下一個範圍的開始值。 例如，如果目前範圍是 5001-6000，則該值為 6001。|  
    |**[最大識別值]**|整數值。 唯讀。|識別欄位的最大值。 由資料行的基底資料型別決定。|  
    |**[遞增]**|整數值。 唯讀。|每次插入時，應增加或是減少的識別欄位的值數量：通常設定為 1。|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要在發行資料表後修改識別範圍和臨界值  
  
1.  在 **文章** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，選取的資料表之 identity 資料行。  
  
2.  按一下 **[發行項屬性]**，然後按一下 **[設定反白顯示資料表發行項的屬性]**。  
  
3.  在 **屬性** ] 索引標籤 **發行項屬性-\< 發行項>** 對話方塊中，於 **身分識別範圍管理** 區段中，輸入一或多個下列屬性的值︰ **發行者範圍大小**, ，**訂閱者範圍大小**, ，和 **範圍臨界值百分比**。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  按一下 [ **確定** 上 **發行集屬性-\< 發行集>** 對話方塊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以在建立發行項時，使用複寫預存程序來指定識別範圍管理選項。  
  
#### 在針對交易式發行集定義發行項時，啟用自動識別範圍管理  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 如果正在發行的來源資料表有識別資料行，指定的值 **自動** 的 **@identityrangemanagementoption**, ，指派給發行者的身分識別值的範圍 **@pub_identity_range**, ，指派給每個訂閱者的身分識別值範圍 **@identity_range**, ，並指派新識別範圍之前所使用的總識別值的百分比 **@threshold**。 如需有關如何定義發行項的詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  請確定識別欄位的資料類型夠大，足以支援指派給所有訂閱者的識別總範圍。  
  
#### 在針對交易式發行集定義發行項時，停用自動識別範圍管理  
  
1.  在發行集資料庫的發行者，執行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定的值為 **手動** 的 **@identityrangemanagementoption**。 如需有關如何定義發行項的詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在訂閱者上指派識別發行項欄位的範圍，以免產生更新訂閱者的衝突。 如需詳細資訊，請參閱區段上為 > 主題中的手動識別範圍管理指派範圍 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
#### 在針對合併式發行集定義發行項時，啟用自動識別範圍管理  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 如果正在發行的來源資料表有識別資料行，指定其值為 **自動** 的 **@identityrangemanagementoption**, ，指派給伺服器訂閱的識別值的範圍 **@pub_identity_range**, ，指派給 「 發行者 」 與每個用戶端訂閱的識別值的範圍 **@identity_range**, ，並指派新識別範圍之前所使用的總識別值的百分比 **@threshold**。 當指派新識別範圍的詳細資訊，請參閱主題中的指派識別範圍 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。 如需有關如何定義發行項的詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
    > [!NOTE]  
    >  請確定識別欄位的資料類型夠大，足以支援指派給所有訂閱者的識別總範圍，特別是具有伺服器訂閱的訂閱者  
  
#### 在針對合併式發行集定義發行項時，停用自動識別範圍管理  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定下列值的其中一個 **@identityrangemanagementoption**:  
  
    -   **手動** -您必須手動指派識別範圍，更新訂閱者。  
  
    -   **無** -在發行者端的識別欄位將不會定義為訂閱者端的識別資料行。  
  
     如需有關如何定義發行項的詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
2.  在訂閱者上指派識別發行項欄位的範圍，以免產生更新訂閱者的衝突。  
  
#### 針對快照式或交易式發行集中的現有發行項，變更自動識別範圍管理設定  
  
1.  在發行集資料庫的發行者，執行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) ，並記下的值 **identityrangemanagementoption** 結果集中。 如果此值為 **0**, ，未啟用自動識別範圍管理。  
  
2.  如果值 **identityrangemanagementoption** 結果集是 **1**, ，變更設定，如下所示︰  
  
    -   若要變更指派的識別範圍，請執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **identity_range** 或 **pub_identity_range** 的 **@property** 和新的範圍值 **@value**。  
  
    -   若要變更指派新範圍的臨界值，請執行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **閾值** 的 **@property** 和新的臨界值，如 **@value**。  
  
#### 針對合併式發行集中的現有發行項，變更自動識別範圍管理設定  
  
1.  在發行集資料庫的發行者，執行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) ，並記下的值 **identity_support** 結果集中。 如果此值為 **0**, ，未啟用自動識別範圍管理。  
  
2.  如果值 **identity_support** 結果集是 **1**, ，變更設定，如下所示︰  
  
    -   若要變更指派的識別範圍，請執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **identity_range** 或 **pub_identity_range** 的 **@property** 和新的範圍值 **@value**。  
  
    -   若要變更指派新範圍的臨界值，請執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **閾值** 的 **@property** 和新的臨界值，如 **@value**。 當指派新識別範圍的詳細資訊，請參閱主題中的指派識別範圍 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
    -   若要停用自動識別範圍管理，請執行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **identityrangemanagementoption** 的 **@property** 和 **手動** 或 **無** 的 **@value**。  
  
## 另請參閱  
 [點對點異動複寫](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  