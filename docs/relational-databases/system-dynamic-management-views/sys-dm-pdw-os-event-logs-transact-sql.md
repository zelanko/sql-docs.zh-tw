---
title: sys.dm_pdw_os_event_logs (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a0daa8cf-72e2-4349-8be1-d3cc0f9b1e02
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 819b38bce871bd1a43b3d259d23b2c95fb6dfdd3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086216"
---
# <a name="sysdmpdwoseventlogs-transact-sql"></a>sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存不同的節點上的不同的 Windows 事件的相關資訊記錄檔。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|此記錄檔的來源應用裝置節點。<br /><br /> pdw_node_id 和 log_name 形成這個檢視的索引鍵。||  
|log_name|**nvarchar(255)**|Windows 事件記錄檔名稱。<br /><br /> pdw_node_id 和 log_name 形成這個檢視的索引鍵。||  
|log_source|**nvarchar(255)**|Windows 事件記錄檔來源的名稱。||  
|event_id|**int**|事件的識別碼。 不是唯一的。||  
|event_type|**nvarchar(255)**|識別嚴重性的事件類型。|「 資訊 」，'Warning'、 'Error'|  
|event_message|**nvarchar(4000)**|事件的詳細資料。||  
|generate_time|**datetime**|建立事件的時間。||  
|write_time|**datetime**|事件實際寫入至記錄檔的時間。||  
  
 這份檢視所保留的最大資料列的相關資訊，請參閱中的 [中繼資料] 區段[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主題。 
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
