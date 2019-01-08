---
title: IHextendedSubscriptionView (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedSubscriptionView_TSQL
- IHextendedSubscriptionView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedSubscriptionView view
ms.assetid: 124756a4-463a-4a81-bf5b-de7e8ffc7a62
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30ba4a0947f98ab34ed8c11ef0e8f3a25c3e453b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756980"
---
# <a name="ihextendedsubscriptionview-transact-sql"></a>IHextendedSubscriptionView (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHextendedSubscriptionView**檢視會公開非 SQL Server 發行集的訂用帳戶上的資訊。 這份檢視儲存在**發佈**資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**article_id**|**int**|發行項的唯一識別碼。|  
|**dest_db**|**sysname**|目的地資料庫的名稱。|  
|**srvid**|**smallint**|訂閱者的唯一識別碼。|  
|**login_name**|**sysname**|用來連接到訂閱者的登入。|  
|**distribution_jobid**|**binary**|識別散發代理程式作業。|  
|**publisher_database_id**|**int**|識別發行集資料庫。|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> **0** = 發送-散發代理程式執行於訂閱者。<br /><br /> **1** = 提取-散發代理程式執行於散發者。|  
|**sync_type**|**tinyint**|初始同步處理的類型：<br /><br /> **1** = 自動<br /><br /> **2** = 無|  
|**status**|**tinyint**|訂閱的狀態：<br /><br /> **0** = 非使用中<br /><br /> **1** = 訂閱<br /><br /> **2** = 作用中|  
|**snapshot_seqno_flag**|**bit**|指出快照集序號是否在使用中。|  
|**independent_agent**|**bit**|指定這個發行集是否有獨立的散發代理程式。<br /><br /> **0** = 發行集使用共用的散發代理程式，以及每一組發行者資料庫/訂閱者資料庫都有單一共用代理程式。<br /><br /> **1** = 沒有獨立的散發代理程式，針對這個發行集。|  
|**subscription_time**|**datetime**|僅供內部使用。|  
|**loopback_detection**|**bit**|適用於雙向異動複寫拓撲中的訂閱。 回送偵測會判斷散發代理程式是否將起源於訂閱者端的交易傳回給訂閱者：<br /><br /> **1** = 不傳回。<br /><br /> **0** = 傳回。|  
|**agent_id**|**int**|散發代理程式的唯一識別碼。|  
|**update_mode**|**tinyint**|指出更新模式的類型，它可以是下列項目之一：<br /><br /> **0** = 唯讀。<br /><br /> **1** = 立即更新。<br /><br /> **2** = 使用 Message Queuing 的佇列更新。<br /><br /> **3** = 立即更新與佇列更新進行容錯移轉使用訊息佇列。<br /><br /> **4** = 使用 SQL Server 佇列的佇列更新。<br /><br /> **5** = 立即更新與佇列的更新容錯移轉時，使用 SQL Server 佇列。|  
|**publisher_seqno**|**varbinary(16)**|這項訂閱在發行者端的交易序號。|  
|**ss_cplt_seqno**|**varbinary(16)**|用來指定並行快照集處理完成的序號。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
