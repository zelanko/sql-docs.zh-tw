---
title: M (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_sessions
- MSmerge_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_sessions system table
ms.assetid: 09ada8fc-c148-4379-9524-7826b1b0216c
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 652baa9f09358c4ee37263522aba52ff72658c6a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="msmergesessions-transact-sql"></a>MSmerge_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSmerge_sessions**資料表包含記錄資料列先前合併代理程式作業工作階段的結果。 每次執行合併代理程式時，都會在這個資料中加入一個新的資料列。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|合併代理程式作業工作階段的識別碼。|  
|**agent_id**|**int**|合併代理程式的識別碼。|  
|**start_time**|**datetime**|作業開始執行的時間。|  
|**end_time**|**datetime**|作業執行完成的時間。|  
|**duration**|**int**|這個作業工作階段的累加持續時間 (以秒為單位)。|  
|**delivery_time**|**int**|套用變更批次所花的秒數。|  
|**upload_time**|**int**|將變更上傳到發行者所花的秒數。|  
|**download_time**|**int**|將變更下載到訂閱者所花的秒數。|  
|**delivery_rate**|**float**|每秒傳遞的平均命令數目。|  
|**time_remaining**|**int**|使用中的工作階段其餘的估計秒數。|  
|**percent_complete**|**decimal**|使用中的工作階段已傳遞的總變更估計百分比。|  
|**upload_inserts**|**int**|發行者端所套用的插入數目。|  
|**upload_updates**|**int**|發行者端所套用的更新數目。|  
|**upload_deletes**|**int**|發行者端所套用的刪除數目。|  
|**upload_conflicts**|**int**|在發行者端套用變更時，所發生的衝突數目。|  
|**upload_conflicts_resolved**|**int**|在發行者端套用變更時，所發生且已解決的衝突數目。|  
|**upload_rows_retried**|**int**|上傳到發行者且已重試的資料列數。|  
|**download_inserts**|**int**|訂閱者端所套用的插入數目。|  
|**download_updates**|**int**|訂閱者端所套用的更新數目。|  
|**download_deletes**|**int**|訂閱者端所套用的刪除數目。|  
|**download_conflicts**|**int**|在訂閱者端套用變更時，所發生的衝突數目。|  
|**download_conflicts_resolved**|**int**|在訂閱者端套用變更時，所發生且已解決的衝突數目。|  
|**download_rows_retried**|**int**|下載到訂閱者且已重試的資料列數。|  
|**schema_changes**|**int**|工作階段期間所套用的結構描述變更數目。|  
|**metadata_rows_cleanedup**|**int**|工作階段期間在期間，清除中繼資料的資料列數。|  
|**runstatus**|**int**|執行狀態如下：<br /><br /> **1** = 開始。<br /><br /> **2** = 成功。<br /><br /> **3** = 進行中。<br /><br /> **4** = 閒置。<br /><br /> **5** = 重試。<br /><br /> **6** = 失敗。|  
|**estimated_upload_changes**|**int**|發行者端必須套用的估計變更數目。|  
|**estimated_download_changes**|**int**|訂閱者端必須套用的估計變更數目。|  
|**connection_type**|**int**|上傳期間所用的連接：<br /><br /> **1** = 區域網路 (LAN)。<br /><br /> **2** = 撥號網路連接。<br /><br /> **3** = web 同步處理。|  
|**timestamp**|**timestamp**|這份資料表的時間戳記資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
