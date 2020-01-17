---
title: 啟用交易式發行集的可更新訂閱
description: 了解如何在 SQL Server 中啟用交易式發行集的可更新訂閱
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, enabling
- subscriptions [SQL Server replication], updatable
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8afde3ebd4082df0c1fc0065b2aa058095905ead
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321247"
---
# <a name="enable-updating-subscriptions-for-transactional-publications"></a>啟用交易式發行集的可更新訂閱
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中啟用交易式發行集的訂閱更新。  
  
> **注意！！** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
 可能的話，會在執行階段提示使用者輸入安全性認證。 如果您必須將認證儲存在指令碼檔案中，則必須維護這個檔案的安全性，使他人無法在未獲授權的情況下擅自存取。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在「新增發行集精靈」的 **[發行集類型]** 頁面上，為交易式發行集啟用更新訂閱。  
  
 若要使用更新訂閱，您還必須在「新增訂閱精靈」中設定選項。  
  
#### <a name="to-enable-updating-subscriptions"></a>若要啟用更新訂閱  
  
1.  在「新增發行集精靈」的 **[發行集類型]** 頁面上，選取 **[具有可更新訂閱的交易式發行集]** 。  
  
2.  在 **[代理程式安全性]** 頁面上，為「佇列讀取器代理程式」、「快照集代理程式」和「記錄讀取器代理程式」指定安全性設定。 如需「佇列讀取器代理程式」執行時使用帳戶所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)＞。  

    > **注意：** 即使您僅使用立即更新訂閱，也會設定「佇列讀取器代理程式」。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 當您以程式設計方式使用複寫預存程序來建立交易式發行集時，可以啟用立即訂閱或佇列更新訂閱。  
  
#### <a name="to-create-a-publication-that-supports-immediate-updating-subscriptions"></a>建立可支援立即更新訂閱的發行集  
  
1.  必要時，請為發行集資料庫建立記錄讀取器代理程式作業。  
  
    -   如果記錄讀取器代理程式作業已存在發行集資料庫中，請繼續進行步驟 2。  
  
    -   如果您不確定發行的資料庫是否有記錄讀取器代理程式作業存在，請在發行集資料庫的發行者端執行 [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)。 如果結果集是空的，就必須建立記錄讀取器代理程式作業。  
  
    -   在發行者端，執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 為 **\@job_name** 和 **\@password** 指定執行代理程式所使用的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 認證。 如果代理程式會在連接到發行者時使用 SQL Server 驗證，您也必須為 **\@publisher_security_mode** 指定 **0** 值，並為 **\@publisher_login** 和 **\@publisher_password**指定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的登入資訊。  
  
2.  執行 [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)，為 **\@allow_sync_tran** 參數指定 **true** 值。  
  
3.  在發行者端，執行 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 為 **\@publication** 指定步驟 2 中所使用的發行集名稱，並為 **\@job_name** 和 **\@password** 指定快照集代理程式執行時所使用的 Windows 認證。 如果代理程式會在連接到發行者時使用 SQL Server 驗證，您也必須為 **\@publisher_security_mode** 指定 **0** 值，並為 **\@publisher_login** 和 **\@publisher_password** 指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的登入資訊。 這麼做會為發行集建立快照集代理程式作業。  
  
4.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
5.  在訂閱者上，建立此發行集的更新訂閱。   
  
#### <a name="to-create-a-publication-that-supports-queued-updating-subscriptions"></a>建立可支援佇列更新訂閱的發行集  
  
1.  必要時，請為發行集資料庫建立記錄讀取器代理程式作業。  
  
    -   如果記錄讀取器代理程式作業已存在發行集資料庫中，請繼續進行步驟 2。  
  
    -   如果您不確定發行的資料庫是否有記錄讀取器代理程式作業存在，請在發行集資料庫的發行者端執行 [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)。 如果結果集是空的，就必須建立記錄讀取器代理程式作業。  
  
    -   在發行者端，執行 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 為 **\@job_name** 和 **\@password** 指定執行代理程式所使用的 Windows 認證。 如果代理程式會在連接到發行者時使用 SQL Server 驗證，您也必須為 **\@publisher_security_mode** 指定 **0** 值，並為 **\@publisher_login** 和 **\@publisher_password** 指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的登入資訊。  
  
2.  必要時，請為散發者建立佇列讀取器代理程式作業。  
  
    -   如果佇列讀取器代理程式作業已存在散發資料庫中，請繼續進行步驟 3。  
  
    -   如果您不確定散發資料庫是否有佇列讀取器代理程式作業存在，請在散發資料庫的散發者上執行 [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)。 如果結果集是空的，就必須建立佇列讀取器代理程式作業。  
  
    -   在散發者端，執行 [sp_addqreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)。 為 **\@job_name** 和 **\@password** 指定執行代理程式所使用的 Windows 認證。 當佇列讀取器代理程式連接到發行者和訂閱者時，會使用這些認證。 如需詳細資訊，請參閱 [複寫代理程式安全性模型](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
3.  執行 [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)，並為 **\@allow_queued_tran** 參數指定 **true** 值，以及為 **\@conflict_policy** 指定 **pub wins**、**sub reinit** 或 **sub wins** 值。  
  
4.  在發行者端，執行 [sp_addpublication_snapshot (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 為 **\@publication** 指定步驟 3 中所使用的發行集名稱，並為 **\@snapshot_job_name** 和 **\@password** 指定快照集代理程式執行時所使用的 Windows 認證。 如果代理程式會在連接到發行者時使用 SQL Server 驗證，您也必須為 **\@publisher_security_mode** 指定 **0** 值，並為 **\@publisher_login** 和 **\@publisher_password** 指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的登入資訊。 這麼做會為發行集建立快照集代理程式作業。  
  
5.  將發行項加入至發行集。 如需詳細資訊，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
6.  在訂閱者上，建立此發行集的更新訂閱。  
  
#### <a name="to-change-the-conflict-policy-for-a-publication-that-allows-queued-updating-subscriptions"></a>針對允許佇列更新訂閱的發行集變更衝突原則  
  
1.  在發行集資料庫的發行者端，執行 [sp_changepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 為 **\@property** 指定 **conflict_policy** 的值，並為 **\@value** 指定 **pub wins**、**sub reinit** 或 **sub wins** 所需的衝突原則模式。  
  
###  <a name="TsqlExample"></a> 範例 &#40;Transact-SQL&#41;  
 此範例會建立一個發行集，它同時支援立即訂閱和佇列更新提取訂閱。  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [設定佇列的更新衝突解決選項 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [異動複寫](../../../relational-databases/replication/transactional/transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)   
 [Create an Updatable Subscription to a Transactional Publication](create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [以指令碼變數使用 sqlcmd](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
