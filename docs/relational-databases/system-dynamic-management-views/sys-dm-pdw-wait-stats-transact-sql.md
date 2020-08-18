---
description: 'sys. dm_pdw_wait_stats (Transact-sql) '
title: sys. dm_pdw_wait_stats (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: f5a8d40b7181f932f5e42192224e91f5c6aa4c8a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88397824"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>sys. dm_pdw_wait_stats (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  保存與在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不同節點上執行之實例相關的作業系統狀態相關資訊。 如需等候類型及其描述的清單，請參閱 [sys. dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|此專案所參考的節點識別碼。||  
|**wait_name**|**nvarchar(255)**|等候類型的名稱。||  
|**max_wait_time**|**bigint**|這種等候類型的等候時間上限。||  
|**request_count**|**bigint**|這種等候類型未完成的等候次數。||  
|**signal_time**|**bigint**|從等候執行緒接獲訊號到開始執行的時間。||  
|**completed_count**|**bigint**|自上次伺服器重新開機之後，已完成的等候總數。||  
|**wait_time**|**bigint**|這種等候類型在 millisecons 中的總等候時間。 包含 signal_time。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys. dm_pdw_waits &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
