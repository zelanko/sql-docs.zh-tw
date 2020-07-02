---
title: MSdynamicsnapshotjobs （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4332e97db70dbbb7254f9cee0863d746f638988e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753889"
---
# <a name="msdynamicsnapshotjobs-transact-sql"></a>MSdynamicsnapshotjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSdynamicsnapshotjobs**資料表會追蹤已套用的參數化資料列篩選器資訊，以產生篩選的資料快照集。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**id**|**int**|篩選資料快照集作業的識別碼。|  
|**name**|**sysname**|篩選資料快照集作業的名稱。|  
|**pubid**|**uniqueidentifier**|這個發行集的唯一識別碼。|  
|**job_id**|**uniqueidentifier**|散發者的 SQL Server Agent 作業的識別碼。|  
|**agent_id**|**int**|SQL Server Agent 的識別碼。|  
|**dynamic_filter_login**|**sysname**|用於評估針對發行集所定義之參數化資料列篩選器中[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)函數的值。|  
|**dynamic_filter_hostname**|**sysname**|用於評估針對發行集所定義之參數化資料列篩選器中[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函數的值。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|如果使用已篩選資料快照集的話，便是要讀取之快照集檔案的資料夾路徑。|  
|**partition_id**|**int**|作業所屬的資料分割識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
