---
description: 'sys.dm_pdw_hadoop_operations (Transact-sql) '
title: sys.dm_pdw_hadoop_operations (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: d86092480b71c6971a72f70fe8b00b4fd10c497e
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834360"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  針對 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 在外部 Hadoop 資料表上執行查詢的過程中，會將每個對應的地圖縮減作業的資料列，推送至 Hadoop。 每個對應-減少作業都代表查詢中的其中一個述詞。 只有在啟用述詞下推以進行 Hadoop 外部資料表的查詢時，才會使用這個。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此外部 Hadoop 作業的識別碼。|與 [sys.dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)中的識別碼相同。|  
|step_index|**int**|參考此 Hadoop 作業的查詢步驟索引。|與 [sys.dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 step_index 相同。|  
|operation_type|**nvarchar(255)**|描述外部操作的類型。|「外部 Hadoop 作業」|  
|operation_name|**nvarchar(4000)**|地圖-減少作業的工作識別碼。 這是在提交作業之後由 Hadoop 傳回 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 的。||  
|map_progress|**float**|對應工作到目前為止已耗用的輸入資料百分比。|介於、和包含0和100之間的浮點數。|  
|reduce_progress|**int**|已完成的縮減作業百分比。|介於、和包含0和100之間的浮點數。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視 ](../../t-sql/language-reference.md)  
  
