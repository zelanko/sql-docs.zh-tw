---
title: sys.databases dm_pdw_wait_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2d5815783528b89716cc8bfb426ea7c1b274802e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68088725"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>sys.databases dm_pdw_wait_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存與在不同節點[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上執行之實例相關的 OS 狀態相關資訊。 如需等候類型及其描述的清單，請參閱[sys.databases dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|此專案所參考之節點的識別碼。||  
|**wait_name**|**nvarchar(255)**|等候類型的名稱。||  
|**max_wait_time**|**bigint**|此等候類型的等候時間上限。||  
|**request_count**|**bigint**|此等候類型未處理的等候次數。||  
|**signal_time**|**bigint**|從等候執行緒接獲訊號到開始執行的時間。||  
|**completed_count**|**bigint**|自從上次伺服器重新開機後，此類型已完成的等候總次數。||  
|**wait_time**|**bigint**|Millisecons 中此等候類型的總等候時間。 包含 signal_time。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [dm_pdw_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
