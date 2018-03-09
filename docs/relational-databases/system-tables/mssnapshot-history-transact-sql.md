---
title: "Y (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsnapshot_history
- MSsnapshot_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsnapshot_history system table
ms.assetid: 56bf4128-1689-4963-9343-432dd0898d31
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbbcdba6941fef9b1890b280f5e7a1efe44161ac
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="mssnapshothistory-transact-sql"></a>MSsnapshot_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsnapshot_history**資料表包含記錄資料列與本機散發者相關聯的快照集代理程式。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|快照集代理程式的識別碼。|  
|**runstatus**|**int**|執行狀態如下：<br /><br /> **1** = 開始。<br /><br /> **2** = 成功。<br /><br /> **3** = 進行中。<br /><br /> **4** = 閒置。<br /><br /> **5** = 重試。<br /><br /> **6** = 失敗。|  
|**start_time**|**datetime**|開始執行作業的時間。|  
|**time**|**datetime**|記錄訊息的時間。|  
|**duration**|**int**|訊息工作階段的持續時間 (以秒為單位)。|  
|**註解**|**nvarchar(255)**|訊息文字。|  
|**delivered_transactions**|**int**|在工作階段所傳遞的交易總數。|  
|**delivered_commands**|**int**|每秒傳遞的命令數。|  
|**delivery_rate**|**float(53)**|平均每秒傳遞的命令數。|  
|**error_id**|**int**|中的錯誤訊息的識別碼[MSrepl_errors](../../relational-databases/system-tables/msrepl-errors-transact-sql.md)系統資料表。|  
|**timestamp**|**timestamp**|這份資料表的時間戳記資料行。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
