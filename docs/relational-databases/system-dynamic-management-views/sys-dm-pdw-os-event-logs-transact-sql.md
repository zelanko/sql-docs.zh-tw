---
title: sys.databases dm_pdw_os_event_logs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ed27e25a1aa977c8fc78186ae2bc9f96ee0e231e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82819270"
---
# <a name="sysdm_pdw_os_event_logs-transact-sql"></a>sys.databases dm_pdw_os_event_logs （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存不同節點上不同 Windows 事件記錄檔的相關資訊。  
  
|資料行名稱|資料類型|說明|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|此記錄檔來源的設備節點。<br /><br /> pdw_node_id 和 log_name 形成此視圖的索引鍵。||  
|log_name|**nvarchar(255)**|Windows 事件記錄檔名稱。<br /><br /> pdw_node_id 和 log_name 形成此視圖的索引鍵。||  
|log_source|**nvarchar(255)**|Windows 事件記錄檔來源名稱。||  
|event_id|**int**|事件的識別碼。 不是唯一的。||  
|event_type|**nvarchar(255)**|事件的類型，識別嚴重性。|[資訊]、[警告]、[錯誤]|  
|event_message|**nvarchar(4000)**|事件的詳細資料。||  
|generate_time|**datetime**|建立事件的時間。||  
|write_time|**datetime**|事件實際寫入記錄檔的時間。||  
  
 如需此視圖所保留之最大資料列的詳細資訊，請參閱[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題中的 Metadata 一節。 
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
