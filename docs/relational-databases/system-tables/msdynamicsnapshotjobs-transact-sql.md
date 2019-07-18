---
title: MSdynamicsnapshotjobs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotjobs_TSQL
- MSdynamicsnapshotjobs
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotjobs system table
ms.assetid: 4f36a325-0e3c-46c4-aeeb-416346cce0bc
author: stevestein
ms.author: sstein
ms.openlocfilehash: f8822b0e7c56fe109a251365050f5aed9cdef178
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907362"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdynamicsnapshotjobs**資料表會追蹤產生篩選的資料快照集的參數化資料列篩選器資訊。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|篩選資料快照集作業的識別碼。|  
|**name**|**sysname**|篩選資料快照集作業的名稱。|  
|**pubid**|**uniqueidentifier**|這個發行集的唯一識別碼。|  
|**job_id**|**uniqueidentifier**|在散發者上的 SQL Server Agent 作業的識別碼。|  
|**agent_id**|**int**|SQL Server Agent 的識別碼。|  
|**dynamic_filter_login**|**sysname**|值，用來評估[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)針對發行集定義的參數化資料列篩選器中的函式。|  
|**dynamic_filter_hostname**|**sysname**|值，用來評估[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)針對發行集定義的參數化資料列篩選器中的函式。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|如果使用已篩選資料快照集的話，便是要讀取之快照集檔案的資料夾路徑。|  
|**partition_id**|**int**|作業所屬的資料分割識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
