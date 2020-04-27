---
title: sys.databases dm_pdw_dms_external_work （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: a1778cbb88fcd6a4142e800cd45109602509125d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899495"
---
# <a name="sysdm_pdw_dms_external_work-transact-sql"></a>sys.databases dm_pdw_dms_external_work （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]此系統檢視會保存外部作業的所有資料移動服務（DMS）步驟的相關資訊。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|使用此 DMS 背景工作的查詢。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|與[sys. dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的 request_id 相同。|  
|step_index|**int**|叫用此 DMS 背景工作角色的查詢步驟。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|與[sys. dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 step_index 相同。|  
|dms_step_index|**int**|DMS 計畫中的目前步驟。<br /><br /> request_id、step_index 和 dms_step_index 會形成此視圖的索引鍵。|與[sys. dm_pdw_dms_workers &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)中的 dms___step_index 相同。|  
|pdw_node_id|**int**|正在執行 DMS 背景工作角色的節點。|與[sys. dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)中的 node_id 相同。|  
|型別|**nvarchar(60)**|此節點正在執行之外部作業的類型。<br /><br /> 檔案分割是外部 Hadoop 檔案的作業，已分割成多個較小的範圍。|「檔案分割」|  
|work_id|**int**|檔案分割識別碼。|大於或等於0。<br /><br /> 每個計算節點都是唯一的。|  
|input_name|**nvarchar(60)**|要讀取之輸入的字串名稱。|針對 Hadoop 檔案，這是 Hadoop 檔案名。|  
|read_location|**bigint**|讀取位置的位移。||  
|estimated_bytes_processed|**bigint**|此工作者所處理的位元組數目。|大於或等於0。|  
|長度|**bigint**|檔案分割中的位元組數目。<br /><br /> 針對 Hadoop，這是 HDFS 區塊的大小。|使用者定義的。 預設值為 64 MB。|  
|status|**nvarchar(32)**|背景工作的狀態。|擱置中、處理中、完成、失敗、已中止|  
|start_time|**datetime**|開始執行此工作者的時間。|大於或等於此工作者所屬查詢步驟的開始時間。 請參閱[dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|end_time|**datetime**|執行結束、失敗或已取消的時間。|針對進行中或佇列的背景工作角色，則為 Null。 否則，大於 start_time。|  
|total_elapsed_time|**int**|花費在執行的總時間（以毫秒為單位）。|大於或等於0。<br /><br /> 如果 total_elapsed_time 超過整數的最大值，total_elapsed_time 會繼續成為最大值。 此狀況會產生「已超過最大值」的警告。<br /><br /> 最大值（以毫秒為單位）相當於24.8 天。|  
  
 如需此視圖所保留之最大資料列的詳細資訊，請參閱[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題中的 Metadata 一節。
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
