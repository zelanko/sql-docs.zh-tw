---
title: sys.dm_pdw_wait_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a62b88ae5c5e0589b54781c85ff43cc39babe2fb
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51667807"
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>sys.dm_pdw_wait_stats & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]OS 狀態與不同節點上執行的執行個體相關。 如需等候的類型和其描述的清單，請參閱 < [sys.dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx)。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|此項目是指的節點的識別碼。||  
|**wait_name**|**nvarchar(255)**|等候類型的名稱。||  
|**max_wait_time**|**bigint**|這種等候類型的最長等待時間。||  
|**request_count**|**bigint**|這個等候次數等候未處理的類型。||  
|**signal_time**|**bigint**|從等候執行緒接獲訊號到開始執行的時間。||  
|**completed_count**|**bigint**|重新啟動之最後一部伺服器之後完成此類型的等候的總數目。||  
|**wait_time**|**bigint**|這種等候類型 millisecons 中的總等候時間。 內含的 signal_time。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
