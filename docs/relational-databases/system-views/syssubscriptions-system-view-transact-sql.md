---
title: syssubscriptions （系統檢視）（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syssubscriptions_TSQL
- syssubscriptions
dev_langs:
- TSQL
helpviewer_keywords:
- syssubscriptions view
ms.assetid: c9613858-9512-43a9-aa53-7ee8064f064c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8162726591f08329ddfc5cb800adece8bfd1fd59
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85692719"
---
# <a name="syssubscriptions-system-view-transact-sql"></a>syssubscriptions (系統檢視) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **Syssubscriptions** view 會公開訂用帳戶資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|訂閱之發行項的唯一識別碼。|  
|**srvid**|**smallint**|訂閱者的伺服器識別碼。|  
|**dest_db**|**sysname**|訂閱資料庫的名稱。|  
|**status**|**tinyint**|訂閱的狀態：<br /><br /> **0** = 非使用中。<br /><br /> **1** = 已訂閱。<br /><br /> **2** = 使用中。|  
|**sync_type**|**tinyint**|初始同步處理的類型：<br /><br /> **1** = 自動。<br /><br /> **2** = 無。|  
|**login_name**|**sysname**|在連接到發行者以加入訂閱時，所用的登入名稱。|  
|**subscription_type**|**int**|訂閱的類型：<br /><br /> **0** = 推播-散發代理程式會在散發者端執行。<br /><br /> **1** = 提取-散發代理程式在訂閱者端執行。|  
|**distribution_jobid**|**binary(16)**|識別同步處理訂閱所用的散發代理程式作業。|  
|**timestmap**|**timestamp**|建立訂閱的日期和時間。|  
|**update_mode**|**tinyint**|更新模式：<br /><br /> **0** = 唯讀。<br /><br /> **1** = 立即更新。|  
|**loopback_detection**|**bit**|適用於雙向異動複寫拓撲中的訂閱。 回送偵測會判斷散發代理程式是否將起源於訂閱者端的交易傳回給訂閱者：<br /><br /> **0** = 傳回。<br /><br /> **1** = 不傳回。|  
|**queued_reinit**|**bit**|指定發行項是否標示初始化或重新初始化。 值為**1**時，表示訂閱的發行項已標示為要初始化或重新初始化。|  
|**nosync_type**|**tinyint**|訂閱初始化的類型：<br /><br /> **0** = 自動（快照集）<br /><br /> **1** = 僅複寫支援<br /><br /> **2** = 使用備份進行初始化<br /><br /> **3** = 從記錄序號初始化（LSN）<br /><br /> 如需詳細資訊，請參閱[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)的** \@ sync_type**參數。<br /><br /> **第** = [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**srvname**|**sysname**|訂閱者的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [&#40;Transact-sql&#41;的複寫視圖](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [syssubscriptions &#40;Transact-SQL&#41;](../../relational-databases/system-tables/syssubscriptions-transact-sql.md)  
  
  
