---
title: MSsubscriptions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriptions_TSQL
- MSsubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriptions system table
ms.assetid: b7e8301d-d115-41f6-8d4f-e0d25f453b25
author: stevestein
ms.author: sstein
ms.openlocfilehash: 51ab87c830d27a2749fdb332c5a13a5b5dd85542
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139705"
---
# <a name="mssubscriptions-transact-sql"></a>MSsubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscriptions**資料表包含一個資料列，每個已發行文章在本機散發者所服務的訂用帳戶中。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|發行者資料庫的識別碼。|  
|**publisher_id**|**smallint**|發行者的識別碼。|  
|**publisher_db**|**sysname**|發行者資料庫的名稱。|  
|**publication_id**|**int**|發行集的識別碼。|  
|**article_id**|**int**|發行項的識別碼。|  
|**subscriber_id**|**smallint**|訂閱者的識別碼。|  
|**subscriber_db**|**sysname**|訂閱資料庫的名稱。|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> **0** = 發送。<br /><br /> **1** = 提取。<br /><br /> **2** = 匿名。|  
|**sync_type**|**tinyint**|同步處理的類型：<br /><br /> **1** = 自動。<br /><br /> **2** = 無同步處理。|  
|**status**|**tinyint**|訂閱的狀態：<br /><br /> **0** = 非使用中。<br /><br /> **1** = 訂閱。<br /><br /> **2** = 作用。|  
|**subscription_seqno**|**varbinary(16)**|快照集交易序號。|  
|**snapshot_seqno_flag**|**bit**|值，表示來源的快照集交易序號**1**表示**subscription_seqno**是快照集序號。|  
|**independent_agent**|**bit**|指出這個發行集是否有獨立的散發代理程式。|  
|**subscription_time**|**datetime**|僅供內部使用。|  
|**loopback_detection**|**bit**|適用於雙向異動複寫拓撲中的訂閱。 回送偵測會判斷散發代理程式是否將起源於訂閱者端的交易傳回給訂閱者：<br /><br /> **1** = 不傳回。<br /><br /> **0** = 傳回。<br /><br /> 注意:此資料行僅支援回溯相容性的雙向複寫功能[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新版本中，應該改用點對點複寫。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
|**agent_id**|**int**|代理程式的識別碼。|  
|**update_mode**|**tinyint**|更新的類型。|  
|**publisher_seqno**|**varbinary(16)**|這項訂閱在發行者端的交易序號。|  
|**ss_cplt_seqno**|**varbinary(16)**|用來指定並行快照集處理完成的序號。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
