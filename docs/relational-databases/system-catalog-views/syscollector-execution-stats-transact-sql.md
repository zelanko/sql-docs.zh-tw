---
title: syscollector_execution_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d4ab4827ab9d9a86936a8562b0e4765b492acd15
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824891"
---
# <a name="syscollector_execution_stats-transact-sql"></a>syscollector_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供收集組或封裝之工作執行的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|識別每個收集組執行。 用來聯結此檢視與其他詳細記錄。 不可為 Null。|  
|**task_name**|**nvarchar(128)**|這項資訊代表之收集組或封裝工作的名稱。 不可為 Null。|  
|**execution_row_count_in**|**int**|在資料流程開頭處理的資料列數目。 可為 Null。|  
|**execution_row_count_out**|**int**|在資料流程結尾處理的資料列數目。 可為 Null。|  
|**execution_row_count_errors**|**int**|在資料流程期間失敗的資料列數目。 可為 Null。|  
|**execution_time_ms**|**int**|待完成之工作所需的時間 (以毫秒為單位)。 可為 Null。|  
|**log_time**|**datetime**|記錄這項資訊的時間。 不可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要**dc_operator**的 SELECT 許可權。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料收集器預存程式](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的資料收集器視圖](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [資料收集](../../relational-databases/data-collection/data-collection.md)  
  
  
