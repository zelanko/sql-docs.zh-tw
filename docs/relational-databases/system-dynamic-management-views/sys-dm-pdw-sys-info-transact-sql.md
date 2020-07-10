---
title: dm_pdw_sys_info (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 93e0020fb0da67538b37c171b3252ba029184554
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197020"
---
# <a name="sysdm_pdw_sys_info-transact-sql"></a>dm_pdw_sys_info (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  提供一組設備層級的計數器，可反映設備上的整體活動。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|目前在系統中的會話數目。|0到 max_active_sessions (請參閱下面) 。|  
|idle_sessions|**int**|目前閒置的會話數目。||  
|active_requests|**int**|目前正在執行的使用中要求數目。||  
|queued_requests|**int**|目前已排入佇列的要求數目。||  
|active_loads|**int**|目前正在系統中執行的載入數目。||  
|queued_loads|**int**|等待執行的佇列載入數目。||  
|active_backups|**int**|目前正在執行的備份數目。||  
|active_restores|**int**|目前正在執行的備份還原數。||  
  
## <a name="see-also"></a>另請參閱  
 [SQL 資料倉儲和平行處理資料倉儲動態管理 Views &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
