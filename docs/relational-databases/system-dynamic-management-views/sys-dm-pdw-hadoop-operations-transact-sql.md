---
title: dm_pdw_hadoop_operations (Transact-sql) |Microsoft Docs
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
ms.openlocfilehash: 6378ddd4b0604fabe81d669d272b59207781fdf8
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197079"
---
# <a name="sysdm_pdw_hadoop_operations-transact-sql"></a>dm_pdw_hadoop_operations (Transact-sql) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  包含每個對應的資料列-在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 外部 Hadoop 資料表上執行查詢時，會向下推送至 Hadoop 的作業。 每個對應-「減少」作業都代表查詢中的其中一個述詞。 只有在已針對 Hadoop 外部資料表上的查詢啟用述詞下推時，才會使用此功能。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此外部 Hadoop 作業的識別碼。|與 sys.databases 中的識別碼相同[dm_pdw_exec_requests &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|參考此 Hadoop 作業的查詢步驟索引。|與[sys. dm_pdw_request_steps &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)中的 step_index 相同。|  
|operation_type|**nvarchar(255)**|描述外部運算的類型。|「外部 Hadoop 作業」|  
|operation_name|**nvarchar(4000)**|地圖-縮減作業的作業識別碼。 這是由 Hadoop 在 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 提交作業之後傳回。||  
|map_progress|**float**|對應工作目前為止已耗用的輸入資料百分比。|介於、和之間的浮點數，包括0和100。|  
|reduce_progress|**int**|已完成的縮減作業百分比。|介於、和之間的浮點數，包括0和100。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統檢視](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
