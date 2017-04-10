---
title: "設定訂閱的逾期期限 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "訂閱 [SQL Server 複寫], 逾期"
  - "逾期 [SQL Server 複寫]"
  - "保留週期 [SQL Server 複寫]"
  - "停用訂閱"
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 設定訂閱的逾期期限
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中設定訂閱的逾期期限。 訂閱的逾期期限可決定訂閱到期及移除之前的期間。 如需詳細資訊，請參閱 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
-   **若要設定訂閱的逾期期限，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   訂閱過期期間也稱為 *「發行集保留期限」*。 清除合併式複寫的中繼資料取決於此設定：  
  
    -   複寫無法在發行集和訂閱資料庫中清除中繼資料，直到到達保留期限為止。 小心指定保留期限的高數值，因為此值可能對複寫效能產生負面影響。 若您能夠確實預測所有訂閱者都會在該時間週期內定期同步處理，建議您使用較低設定。  
  
         合併式發行集的保留期限具有 24 小時寬限期，可配合不同時區的「訂閱者」。 例如，如果您設定的保留期限是一天，實際的保留期限便是 48 小時。  
  
    -   您可以將訂閱指定為永不過期，不過強烈建議您不要使用此值，因為如此便無法清除中繼資料了。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 設定訂閱的逾期期限 **一般** 頁面 **發行集屬性-\< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
#### 若要設定訂閱的過期期間  
  
1.  在 **訂閱過期** 區段 **一般** 頁面 **發行集屬性-\< 發行集>** 對話方塊方塊中，指定是否應過期的訂閱。  
  
2.  如果應過期，則指定過期期間。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 您可以使用複寫預存程序，在建立發行集時設定這個值，或是在稍後修改這個值。  
  
#### 設定快照式或交易式發行集之訂閱的逾期期限  
  
1.  在 「 發行者 」 執行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 針對 **@retention**指定所要的訂閱逾期期限 (以小時為單位)。 預設的逾期期限為 336 小時。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 設定合併式發行集之訂閱的逾期期限  
  
1.  在 「 發行者 」 執行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 針對 **@retention**指定所要的訂閱逾期期限值。 指定用於表示有效期限的單位 **@retention_period_unit**, ，它可以是下列其中之一︰  
  
    -   **1** = 週  
  
    -   **2** = 月  
  
    -   **3** = 年  
  
     預設的逾期期限為 14 天。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 變更快照式或交易式發行集之訂閱的逾期期限  
  
1.  在 「 發行者 」 執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 針對 **@property** 指定 **retention** ，並針對 **@value**指定新的訂閱逾期期限 (以小時為單位)。  
  
#### 變更合併式發行集之訂閱的逾期期限  
  
1.  在 「 發行者 」 執行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，並指定 **@publication** 和 **@publisher**。 記下的值 **retention_period_unit** 結果集中可以是下列其中一項︰  
  
    -   **0** = 日  
  
    -   **1** = 週  
  
    -   **2** = 月  
  
    -   **3** = 年  
  
2.  在 「 發行者 」 執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 針對 **@property** 指定 **retention** ，並針對 **@value**指定新的訂閱逾期期限 (以步驟 1 中保留期限單位為根據的文字)。  
  
3.  （選擇性）在 「 發行者 」 執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 指定 **retention_period_unit** 的 **@property** 和新的訂閱逾期期限單位 **@value**。  
  
## 另請參閱  
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [訂閱逾期與停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  