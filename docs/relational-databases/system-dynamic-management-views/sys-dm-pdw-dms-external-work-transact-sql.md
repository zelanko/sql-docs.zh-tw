---
title: sys.dm_pdw_dms_external_work (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
caps.latest.revision: 5
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 30865bcccb0085d1b01b61aaef826dc76f081169
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2018
ms.locfileid: "36772083"
---
# <a name="sysdmpdwdmsexternalwork-transact-sql"></a>sys.dm_pdw_dms_external_work & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 保留外部作業的所有資料移動服務 (DMS) 步驟的相關資訊的系統檢視表。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|使用此 DMS 背景工作的查詢。<br /><br /> request_id、 step_index 和 dms_step_index 形成這個檢視的索引鍵。|相同中的 request_id [sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|查詢會叫用這個 DMS 背景工作的步驟。<br /><br /> request_id、 step_index 和 dms_step_index 形成這個檢視的索引鍵。|相同中 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|dms_step_index|**int**|目前在 DMS 計劃中的步驟。<br /><br /> request_id、 step_index 和 dms_step_index 形成這個檢視的索引鍵。|相同中 dms___step_index [sys.dm_pdw_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)。|  
|pdw_node_id|**int**|執行 DMS 背景工作角色的節點。|相同的 node_id [sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)。|  
|型別|**nvarchar(60)**|此節點正在執行的外部作業類型。<br /><br /> 分割檔案是已分割成多個較小的落在外部 Hadoop 檔案上作業。|' 檔案分割 '|  
|work_id|**int**|分割的檔案識別碼。|大於或等於 0。<br /><br /> 每個計算節點是唯一的。|  
|input_name|**nvarchar(60)**|正在讀取的輸入名稱的字串。|Hadoop 檔案，這是 Hadoop 檔案名稱。|  
|read_location|**bigint**|讀取位置的位移。||  
|estimated_bytes_processed|**bigint**|這個工作者所處理的位元組數目。|大於或等於 0。|  
|長度|**bigint**|分割的檔案中的位元組數目。<br /><br /> 適用於 Hadoop，這是 HDFS 區塊的大小。|使用者定義。 預設值是 64 MB。|  
|status|**nvarchar(32)**|背景工作的狀態。|暫止，處理、 完成、 失敗、 已中止|  
|start_time|**datetime**|此工作者執行的開始時間。|大於或等於此背景工作所屬的查詢步驟的開始時間。 請參閱[sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|在執行結束、 失敗或已取消的時間。|進行中或已排入佇列的背景工作角色為 NULL。 否則，大於 start_time。|  
|total_elapsed_time|**int**|在執行中，以毫秒為單位所花費的總時間。|大於或等於 0。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 仍是最大值。 這種情況會產生警告 」 的最大值已超過 」。<br /><br /> 以毫秒為單位的最大值相當於 24.8 天。|  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱[系統檢視的最大值](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9)。  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
