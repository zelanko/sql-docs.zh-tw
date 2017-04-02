---
title: "切換可更新之交易式訂閱的更新模式 | Microsoft Docs"
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
  - "異動複寫, 可更新的訂閱"
  - "可更新的訂閱, 更新模式"
  - "訂閱 [SQL Server 複寫], 可更新"
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# 切換可更新之交易式訂閱的更新模式
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中切換可更新之交易訂閱的更新模式。 使用「新增訂閱精靈」指定可更新訂閱的模式。 使用此精靈時，將模式設定的相關資訊，請參閱 [檢視和修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
-   **若要切換可更新之交易式訂閱的更新模式，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   您可以隨時從立即更新容錯移轉到到佇列更新。 不過在進行這項作業之後，在「訂閱者」和「發行者」連接，且「佇列讀取器代理程式」將佇列中所有暫止訊息套用至「發行者」之前，無法切換回立即更新。  
  
###  <a name="Recommendations"></a> 建議  
  
-   當交易式訂閱的更新訂閱支援從一種更新模式容錯移轉到另一種模式時，您可以透過程式設計的方式切換更新模式，以處理連接在短時間內變更的情況。 您可以使用複寫預存程序，以程式設計的方式並視需要而設定更新模式。 如需詳細資訊，請參閱 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
> [!NOTE]  
>  若要在建立訂閱之後變更的更新模式 **update_mode** 屬性必須設為 **容錯移轉** （允許從立即更新，以切換佇列更新） 或 **排入佇列的容錯移轉** （允許從立即更新佇列更新的交換器） 建立訂閱時。 這些屬性會自動在「新增訂閱精靈」中設定。  
  
#### 若要設定發送訂閱的更新模式  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的訂閱者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機訂閱]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要設定更新模式，以及 [的訂閱 **設定更新方法**。  
  
4.  在 **設定更新方法-\< 訂閱者>: \< u>** 對話方塊中，選取 **立即更新** 或 **佇列更新**。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 若要設定提取訂閱的更新模式  
  
1.  在 **訂閱屬性-\< 發行者>: \< u>** 對話方塊中，選取值 **立即複寫變更** 或 **佇列變更** 的 **訂閱者更新方法** 選項。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 如需有關存取 **訂閱屬性-\< 發行者>: \< u>** 對話方塊中，請參閱 [檢視和修改提取訂閱屬性](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 切換更新模式  
  
1.  請確認訂閱支援容錯移轉，藉由執行 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) 提取訂閱或 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) 發送訂閱。 如果值 **更新模式** 結果集是 **3** 或 **4**, ，可支援容錯移轉。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，和下列其中一個值 **@failover_mode**:  
  
    -   **已排入佇列** -容錯移轉到佇列更新時的連線已暫時遺失。  
  
    -   **立即** -容錯移轉到立即更新，在恢復連線。  
  
## 另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  