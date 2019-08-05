---
title: 手動初始化訂閱 | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- manual subscription initialization [SQL Server replication]
- subscriptions [SQL Server replication], initializing
- initializing subscriptions [SQL Server replication], without snapshots
ms.assetid: 27a1bc38-e498-4fff-8082-04b52aa4b22c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: eff19816330eb512c48cc6a37237ecf6030d7e4f
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768545"
---
# <a name="initialize-a-subscription-manually"></a>手動初始化訂閱
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中手動初始化訂閱。 當正常使用初始快照集來初始化訂閱時，可以不使用快照集來初始化發行集的訂閱，但前提是訂閱者上已經有結構描述和初始資料。  
  

##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   例如，若在複製資料和結構描述到訂閱者的時間，與手動初始化訂閱的時間之間，使用異動複寫發行的資料庫上有活動，則此活動所導致的變更可能不會複寫到訂閱者。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 透過將結構描述 (通常是資料) 複製到訂閱資料庫的方式，手動初始化發行集的訂閱。 結構描述和資料應與發行集資料庫相符。 然後在「新增訂閱精靈」的 **[初始化訂閱]** 頁面中指定訂閱不需要結構描述和資料。 如需有關存取這個精靈的詳細資訊，請參閱＜ [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) ＞與＜ [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)中手動初始化訂閱。  
  
 您初次同步處理訂閱時，會將複寫所需的物件和中繼資料複製到訂閱資料庫。  
  
#### <a name="to-initialize-a-subscription-to-a-publication-manually"></a>若要手動初始化發行集的訂閱  
  
1.  確定將結構描述和資料複製到訂閱資料庫。  
  
2.  清除「新增訂閱精靈」 **[初始化訂閱]** 頁面中的 **[初始化]** 核取方塊。 只有複製複寫物件和中繼資料時，才需要對每個訂閱執行此操作。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用複寫預存程序來手動初始化訂閱。  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-transactional-publication"></a>手動初始化交易式發行集的提取訂閱  
  
1.  確定訂閱資料庫上有結構描述和資料存在。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
2.  在發行集資料庫的「發行者」上，執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定 **\@publication**、 **\@subscriber**、位於包含 **\@destination_db** 發行資料之訂閱者上的資料庫名稱、為 **\@subscription_type** 指定 **pull** 值，以及為 **\@sync_type** 指定 **replication support only** 值。 如需詳細資訊，請參閱 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
3.  在訂閱者上，執行 [sp_addpullsubscription](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 如需更新訂閱，請參閱＜ [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx)＞。  
  
4.  在訂閱者上，執行 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 如需詳細資訊，請參閱 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
5.  啟動散發代理程式，以傳送複寫物件以及從發行者下載最新的變更。 如需相關資訊，請參閱 [同步處理提取訂閱](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-transactional-publication"></a>手動初始化交易式發行集的發送訂閱  
  
1.  確定訂閱資料庫上有結構描述和資料存在。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。  
  
2.  在發行集資料庫的「發行者」上，執行 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 指定位於包含 **\@destination_db** 發行資料之訂閱者上的資料庫名稱、為 **\@subscription_type** 指定 **push** 值，以及為 **\@sync_type** 指定 **replication support only** 值。 如需更新訂閱，請參閱＜ [Create an Updatable Subscription to a Transactional Publication](https://technet.microsoft.com/library/ms152769(v=sql.130).aspx)＞。  
  
3.  在發行集資料庫的「發行者」上，執行 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 如需詳細資訊，請參閱 [建立發送訂閱](../../relational-databases/replication/create-a-push-subscription.md)。  
  
4.  啟動散發代理程式，以傳送複寫物件以及從發行者下載最新的變更。 如需詳細資訊，請參閱 [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### <a name="to-manually-initialize-a-pull-subscription-to-a-merge-publication"></a>手動初始化合併式發行集的提取訂閱  
  
1.  確定訂閱資料庫上有結構描述和資料存在。 這項處理可以藉由在訂閱者上還原發行集資料庫的備份來完成。  
  
2.  在發行者上，執行 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)。 指定 **\@publication**、 **\@subscriber**、 **\@subscriber_db**，以及為 **\@subscription_type** 指定 **pull** 值。 如此會註冊提取訂閱。  
  
3.  在包含已發行資料之資料庫的訂閱者上，執行 [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 為 **\@sync_type** 指定 **none** 值。  
  
4.  在訂閱者上，執行 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)。 如需詳細資訊，請參閱 [建立提取訂閱](../../relational-databases/replication/create-a-pull-subscription.md)。  
  
5.  啟動合併代理程式，以傳送複寫物件以及從發行者下載最新的變更。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### <a name="to-manually-initialize-a-push-subscription-to-a-merge-publication"></a>手動初始化合併式發行集的發送訂閱  
  
1.  確定訂閱資料庫上有結構描述和資料存在。 這項處理可以藉由在訂閱者上還原發行集資料庫的備份來完成。  
  
2.  在發行集資料庫的發行者上，執行 [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)。 指定位於包含 **\@subscriber_db** 發行資料之訂閱者上的資料庫名稱、為 **\@subscription_type** 指定 **push** 值，以及為 **\@sync_type** 指定 **none** 值。  
  
3.  在發行集資料庫的「發行者」上，執行 [sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)。 如需詳細資訊，請參閱 [建立發送訂閱](../../relational-databases/replication/create-a-push-subscription.md)。  
  
4.  啟動合併代理程式，以傳送複寫物件以及從發行者下載最新的變更。 如需詳細資訊，請參閱 [同步處理發送訂閱](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)   
 [備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
