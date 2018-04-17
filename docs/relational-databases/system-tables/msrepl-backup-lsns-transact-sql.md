---
title: MSrepl_backup_lsns (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
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
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 50584d1c55dd24dbf2722d506b79fe36739ce0f5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="msreplbackuplsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_backup_lsns**資料表包含支援散發資料庫 'sync with backup' 選項的交易記錄序號 (LSN)。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|發行者資料庫的識別碼。|  
|**valid_xact_id**|**varbinary(16)**|要傳給發行者來標示記錄截斷點的交易識別碼。 只有在散發資料庫是 'sync with backup' 模式時，才使用這個項目。 包含已備份的散發資料庫中，最新的複寫交易的識別碼。 記錄讀取器會將它傳給發行者來標示記錄截斷點。|  
|**valid_xact_seqno**|**varbinary(16)**|要傳給發行者來標示記錄截斷點的交易序號。 只有在散發資料庫是 'sync with backup' 模式時，才使用這個項目。 它是已備份的散發資料庫中，最新的複寫交易的記錄序號。 記錄讀取器會將它傳給發行者來標示記錄截斷點。|  
|**next_xact_id**|**varbinary(16)**|備份作業所用的暫存記錄序號。|  
|**nextx_xact_seqno**|**varbinary(16)**|備份作業所用的暫存記錄序號。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
