---
description: 'sys. pdw_loader_backup_runs (Transact-sql) '
title: sys. pdw_loader_backup_runs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: fc85ec89f07359714c4661b3b7c4c8d8d5138b1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490252"
---
# <a name="syspdw_loader_backup_runs-transact-sql"></a>sys. pdw_loader_backup_runs (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  包含中進行中和已完成之備份和還原作業的相關資訊 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ，以及中的進行中和已完成的備份、還原和載入作業的相關資訊 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 。 此資訊在系統重新啟動之後會持續存留。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定備份、還原或負載執行的唯一識別碼。<br /><br /> 此視圖的索引鍵。||  
|NAME|**nvarchar(255)**|若為 load，則為 Null。 備份或還原的選擇性名稱。||  
|submit_time|**datetime**|提交要求的時間。||  
|start_time|**datetime**|作業開始的時間。||  
|end_time|**datetime**|作業已完成、失敗或已取消的時間。||  
|total_elapsed_time|**int**|Start_time 和目前時間之間的總時間，或是已完成、已取消或失敗之執行的 start_time 和 end_time 之間的總時間。|如果 total_elapsed_time 超過整數 (24.8 天（以毫秒為單位）的最大值) ，則會造成具體化失敗，因為溢位。<br /><br /> 以毫秒為單位的最大值相當於24.8 天。|  
|operation_type|**Nvarchar (16) **|載入類型。|「備份」、「載入」、「還原」|  
|mode|**Nvarchar (16) **|執行類型內的模式。|針對 operation_type = **備份**<br />**DIFFERENTIAL**<br />**FULL**<br /><br /> For operation_type = **LOAD**<br />**附加**<br />**重新 載入**<br />**UPSERT**<br /><br /> 針對 operation_type = **RESTORE**<br />**資料庫**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|這項作業內容的資料庫名稱||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|要求操作之使用者的識別碼。||  
|session_id|**nvarchar(32)**|執行作業之會話的識別碼。|請參閱 [sys. dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)中的 session_id。|  
|request_id|**nvarchar(32)**|執行作業的要求識別碼。 若為載入，這是與此載入相關聯的目前或最後一個要求。|請參閱 [sys. dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id。|  
|status|**Nvarchar (16) **|執行的狀態。|「已取消」、「已完成」、「失敗」、「已排入佇列」、「正在執行」|  
|progress|**int**|已完成的百分比。|0 到 100|  
|命令|**nvarchar(4000)**|由使用者所提交之命令的完整文字。|如果超過4000個字元 (計算空間) ，則會截斷。|  
|rows_processed|**bigint**|這項作業中處理的資料列數目。||  
|rows_rejected|**bigint**|這項作業中拒絕的資料列數目。||  
|rows_inserted|**bigint**|插入資料庫資料表中的資料列數目 (s) 做為這項作業的一部分。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲與平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
