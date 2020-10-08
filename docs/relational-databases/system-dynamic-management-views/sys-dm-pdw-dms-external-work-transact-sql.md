---
description: 'sys.dm_pdw_dms_external_work (Transact-sql) '
title: sys.dm_pdw_dms_external_work (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 47345015-f861-451e-97c4-6e1cb81d1922
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8683920e22e8888cc3dc93ffa350a43189116646
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834227"
---
# <a name="sysdm_pdw_dms_external_work-transact-sql"></a>sys.dm_pdw_dms_external_work (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 保存所有資料移動服務的相關資訊的系統檢視 (DMS) 步驟進行外部作業。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|使用這個 DMS 背景工作角色的查詢。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|與 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id 相同。|  
|step_index|**int**|正在叫用此 DMS 背景工作角色的查詢步驟。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|與 [sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 step_index 相同。|  
|dms_step_index|**int**|DMS 方案中的目前步驟。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|與 [sys.dm_pdw_dms_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)中的 dms___step_index 相同。|  
|pdw_node_id|**int**|正在執行 DMS 背景工作角色的節點。|與 [sys.dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id 相同。|  
|type|**nvarchar(60)**|此節點正在執行的外部作業類型。<br /><br /> 檔案分割是對已分割成多個較小範圍的外部 Hadoop 檔案進行的作業。|「檔案分割」|  
|work_id|**int**|檔案分割識別碼。|大於或等於0。<br /><br /> 每個計算節點都是唯一的。|  
|input_name|**nvarchar(60)**|要讀取之輸入的字串名稱。|針對 Hadoop 檔案，這是 Hadoop 檔案名。|  
|read_location|**bigint**|讀取位置的位移。||  
|estimated_bytes_processed|**bigint**|此背景工作所處理的位元組數目。|大於或等於0。|  
|長度|**bigint**|檔案分割中的位元組數目。<br /><br /> 針對 Hadoop，這是 HDFS 區塊的大小。|使用者定義。 預設值為 64 MB。|  
|status|**nvarchar(32)**|背景工作角色的狀態。|暫止、處理、完成、失敗、已中止|  
|start_time|**datetime**|此背景工作開始執行的時間。|大於或等於此背景工作所屬查詢步驟的開始時間。 請參閱 [sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|執行結束、失敗或已取消的時間。|針對進行中或佇列的背景工作角色為 Null。 否則，大於 start_time。|  
|total_elapsed_time|**int**|花費在執行的總時間（以毫秒為單位）。|大於或等於0。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 將會繼續成為最大值。 這種狀況會產生「已超過最大值」的警告。<br /><br /> 以毫秒為單位的最大值相當於24.8 天。|  
  
 如需此視圖所保留之最大資料列的相關資訊，請參閱「 [容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) 」主題中的「中繼資料」一節。
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](../../t-sql/language-reference.md)  
  
