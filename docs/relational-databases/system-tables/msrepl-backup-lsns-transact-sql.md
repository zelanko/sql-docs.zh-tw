---
title: MSrepl_backup_lsns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_backup_lsns_TSQL
- MSrepl_backup_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_backup_Isns system table
ms.assetid: de06c349-82a8-48c6-b602-b5d6938514f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3c1870e9fba39995f7f8634076c658d8ef044999
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889530"
---
# <a name="msrepl_backup_lsns-transact-sql"></a>MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_backup_lsns**資料表包含交易記錄序號（LSN），可支援散發資料庫的「同步處理與備份」選項。 這份資料表儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|發行者資料庫的識別碼。|  
|**valid_xact_id**|**varbinary(16)**|要傳給發行者來標示記錄截斷點的交易識別碼。 只有在散發資料庫是 'sync with backup' 模式時，才使用這個項目。 包含已備份的散發資料庫中，最新的複寫交易的識別碼。 記錄讀取器會將它傳給發行者來標示記錄截斷點。|  
|**valid_xact_seqno**|**varbinary(16)**|要傳給發行者來標示記錄截斷點的交易序號。 只有在散發資料庫是 'sync with backup' 模式時，才使用這個項目。 它是已備份的散發資料庫中，最新的複寫交易的記錄序號。 記錄讀取器會將它傳給發行者來標示記錄截斷點。|  
|**next_xact_id**|**varbinary(16)**|備份作業所用的暫存記錄序號。|  
|**nextx_xact_seqno**|**varbinary(16)**|備份作業所用的暫存記錄序號。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
