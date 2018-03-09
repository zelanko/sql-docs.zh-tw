---
title: syscollector_execution_stats (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- syscollector_execution_stats
- syscollector_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_execution_stats view
- data collector view
ms.assetid: 23e35ac5-fbbf-4922-970c-f4fac44c1263
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e04c57081f19358786dcc723f6ef2f79757fae2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="syscollectorexecutionstats-transact-sql"></a>syscollector_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供收集組或封裝之工作執行的相關資訊。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|識別每個收集組執行。 用來聯結此檢視與其他詳細記錄。 不可為 Null。|  
|**task_name**|**nvarchar(128)**|這項資訊代表之收集組或封裝工作的名稱。 不可為 Null。|  
|**execution_row_count_in**|**int**|在資料流程開頭處理的資料列數目。 可為 Null。|  
|**execution_row_count_out**|**int**|在資料流程結尾處理的資料列數目。 可為 Null。|  
|**execution_row_count_errors**|**int**|在資料流程期間失敗的資料列數目。 可為 Null。|  
|**execution_time_ms**|**int**|待完成之工作所需的時間 (以毫秒為單位)。 可為 Null。|  
|**log_time**|**datetime**|記錄這項資訊的時間。 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要 SELECT 權限**dc_operator**。  
  
## <a name="see-also"></a>另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [資料收集器檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[資料收集]](../../relational-databases/data-collection/data-collection.md)  
  
  
