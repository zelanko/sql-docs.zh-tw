---
title: syssubscriptions （系統檢視） (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0cab4eb2c04f929a0d161803e36ae7de00fbe01
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (系統檢視) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Syssubscriptions**檢視會公開訂閱資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|訂閱之發行項的唯一識別碼。|  
|**srvid**|**smallint**|訂閱者的伺服器識別碼。|  
|**dest_db**|**sysname**|訂閱資料庫的名稱。|  
|**status**|**tinyint**|訂閱的狀態：<br /><br /> **0** = 非使用中。<br /><br /> **1** = 訂閱。<br /><br /> **2** = 使用。|  
|**sync_type**|**tinyint**|初始同步處理的類型：<br /><br /> **1** = 自動。<br /><br /> **2** = 無。|  
|**login_name**|**sysname**|在連接到發行者以加入訂閱時，所用的登入名稱。|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> **0** = 發送-散發代理程式執行於散發者。<br /><br /> **1** = 提取-散發代理程式執行於訂閱者。|  
|**distribution_jobid**|**binary(16)**|識別同步處理訂閱所用的散發代理程式作業。|  
|**timestmap**|**timestamp**|建立訂閱的日期和時間。|  
|**update_mode**|**tinyint**|更新模式：<br /><br /> **0** = 唯讀。<br /><br /> **1** = 立即更新。|  
|**loopback_detection**|**bit**|適用於雙向異動複寫拓撲中的訂閱。 回送偵測會判斷散發代理程式是否將起源於訂閱者端的交易傳回給訂閱者：<br /><br /> **0** = 傳回。<br /><br /> **1** = 不傳回。|  
|**queued_reinit**|**bit**|指定發行項是否標示初始化或重新初始化。 值為**1**指定標示初始化或重新初始化訂閱的發行項。|  
|**nosync_type**|**tinyint**|訂閱初始化的類型：<br /><br /> **0** = 自動 （快照集）<br /><br /> **1** = 僅支援複寫<br /><br /> **2** = 以備份初始化<br /><br /> **3** = 從記錄序號 (LSN) 初始化<br /><br /> 如需詳細資訊，請參閱**@sync_type**參數[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。<br /><br /> **3** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|訂閱者的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
