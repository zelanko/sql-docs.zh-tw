---
title: sysmergesubscriptions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergesubscriptions_TSQL
- sysmergesubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubscriptions system table
ms.assetid: 6adc78da-991d-4c08-98c3-ecb4762e0e99
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0722ccd8c4f18fd16ed4abdb3630e80bc7d5de53
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824773"
---
# <a name="sysmergesubscriptions-transact-sql"></a>sysmergesubscriptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個已知的訂閱者，各包含一個資料列，這是在發行者端的本機資料表。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|subscriber_server|**sysname**|伺服器的識別碼。 將訂閱資料庫的副本移轉到另一部伺服器時，用來將 srvid 欄位對應至伺服器特定的值。|  
|db_name|**sysname**|訂閱資料庫的名稱。|  
|pubid|**uniqueidentifier**|用來建立目前訂閱的來源發行集識別碼。|  
|datasource_type|**int**|資料來源的類型：<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br /> **2** = Jet OLE DB。|  
|subid|**uniqueidentifier**|訂閱的唯一識別碼。|  
|replnickname|**binary**|複本的精簡暱稱。|  
|replicastate|**uniqueidentifier**|透過比較在「發行者」的值與在「訂閱者」的值，來判斷先前的同步處理是否成功所使用的唯一識別碼。|  
|status|**tinyint**|訂閱的狀態：<br /><br /> **0** = 非使用中。<br /><br /> **1** = 使用中。<br /><br /> **2** = 已刪除。|  
|subscriber_type|**int**|訂閱者的類型：<br /><br /> **1** = 全域。<br /><br /> **2** = 本機。<br /><br /> **3** = 匿名。|  
|subscription_type|**int**|訂閱的類型：<br /><br /> **0** = Push。<br /><br /> **1** = 提取。<br /><br /> **2** = 匿名。|  
|sync_type|**tinyint**|同步處理的類型：<br /><br /> **1** = 自動。<br /><br /> **2** = 無同步處理。|  
|description|**nvarchar(255)**|訂閱的簡要描述。|  
|priority|**real**|指定訂閱優先權，允許實作以優先權為基礎的衝突解決。 所有本機或匿名訂閱都等於**0.00** 。|  
|recgen|**bigint**|收到的最後一個層代 (Generation) 的編號。|  
|recguid|**uniqueidentifier**|收到的最後一個層代 (Generation) 的唯一識別碼。|  
|sentgen|**bigint**|傳送的最後一個層代 (Generation) 的編號。|  
|sentguid|**uniqueidentifier**|傳送的最後一個層代 (Generation) 的唯一識別碼。|  
|schemaversion|**int**|收到的最後一個結構描述的編號。|  
|schemaguid|**uniqueidentifier**|收到的最後一個結構描述的唯一識別碼。|  
|last_validated|**datetime**|最後一次成功驗證訂閱者資料的**日期時間**。|  
|attempted_validate|**datetime**|嘗試在訂閱上進行驗證的最後一個**日期時間**。|  
|last_sync_date|**datetime**|同步處理的**日期時間**。|  
|last_sync_status|**int**|訂閱狀態：<br /><br /> **0** = 所有作業都在等待啟動。<br /><br /> **1** = 一或多個作業正在啟動。<br /><br /> **2** = 所有作業都已順利執行。<br /><br /> **3** = 至少有一項作業正在執行。<br /><br /> **4** = 所有作業都已排程且閒置。<br /><br /> **5** = 在上一次失敗之後，至少有一個作業嘗試執行。<br /><br /> **6** = 至少有一項作業無法順利執行。|  
|last_sync_summary|**sysname**|上次同步處理結果的描述。|  
|metadatacleanuptime|**datetime**|從合併式複寫系統資料表中移除過期中繼資料的最後一個**日期時間**。|  
|partition_id|**int**|識別訂閱所屬的預先計算資料分割。|  
|cleanedup_unsent_changes|**bit**|識別在訂閱者端已清除尚未傳送之變更的中繼資料。|  
|replica_version|**int**|識別訂閱所屬之訂閱者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，它可以是下列其中一個值：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|supportability_mode|**int**|僅供內部使用。|  
|application_name|**nvarchar(128)**|僅供內部使用。|  
|subscriber_number|**int**|僅供內部使用。|  
|last_makegeneration_datetime|**datetime**|Makegeneration 進程針對發行者執行的最後一個**日期時間**。 如需詳細資訊，請參閱[Replication 合併代理程式](../../relational-databases/replication/agents/replication-merge-agent.md)中的-MakeGenerationInterval 參數。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
