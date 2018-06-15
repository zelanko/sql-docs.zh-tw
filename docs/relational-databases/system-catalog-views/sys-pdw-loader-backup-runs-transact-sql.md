---
title: sys.pdw_loader_backup_runs (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 2b72034c-6a11-46b9-a76c-7a88b2bea360
caps.latest.revision: 10
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c9de90ab3777e8f432f29cb16002e629862f12f3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181804"
---
# <a name="syspdwloaderbackupruns-transact-sql"></a>sys.pdw_loader_backup_runs (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含有關進行中和已完成的備份和還原作業中的資訊[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，以及有關進行中和已完成的備份、 還原及載入作業中的[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 此資訊在系統重新啟動之後會持續存留。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|run_id|**int**|特定備份、 還原或負載測試回合的唯一識別碼。<br /><br /> 此檢視的索引鍵。||  
|name|**nvarchar(255)**|負載是 null。 備份或還原的選用名稱。||  
|submit_time|**datetime**|已提交要求的時間。||  
|start_time|**datetime**|作業開始的時間。||  
|end_time|**datetime**|作業已完成、 失敗或已取消的時間。||  
|total_elapsed_time|**int**|總耗用時間之間的 start_time 和 end_time 或之間的 start_time 和目前的時間，已完成、 已取消，或無法執行。|如果 total_elapsed_time 超過整數 （以毫秒為單位的 24.8 天） 的最大值，它會導致具體化失敗，因為發生溢位。<br /><br /> 以毫秒為單位的最大值就相當於 24.8 天。|  
|operation_type|**nvarchar(16)**|載入型別。|'備份'、 '載入'，' RESTORE'|  
|mode|**nvarchar(16)**|在執行的型別中模式。|Operation_type =**備份**<br />**差異**<br />**FULL**<br /><br /> Operation_type =**負載**<br />**附加**<br />**重新載入**<br />**UPSERT**<br /><br /> Operation_type =**還原**<br />**DATABASE**<br />**HEADER_ONLY**|  
|database_name|**nvarchar(255)**|這項作業的內容資料庫的名稱||  
|table_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|Principal_id|**int**|要求作業的使用者識別碼。||  
|session_id|**nvarchar(32)**|執行作業的工作階段識別碼。|請參閱中的 session_id [sys.dm_pdw_exec_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|request_id|**nvarchar(32)**|執行作業之要求的識別碼。 若是載入，這是與此負載關聯的目前或上一個要求...|請參閱中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|status|**nvarchar(16)**|執行狀態。|'取消'，' 填寫 '，'失敗'、 '佇列更新'、 '執行'|  
|進度|**int**|完成的百分比。|0 到 100|  
|command|**nvarchar(4000)**|使用者所提交的命令的完整文字。|如果超過 4000 個字元 （計數為空格） 會被截斷。|  
|rows_processed|**bigint**|這項作業的一部分來處理資料列數目。||  
|rows_rejected|**bigint**|拒絕此作業的資料列數目。||  
|rows_inserted|**bigint**|這項作業的一部份，插入資料庫資料表的資料列數目。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲目錄檢視](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
