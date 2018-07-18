---
title: sys.dm_pdw_hadoop_operations (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.suite: sql
ms.component: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f158ac7c5904e54daf384ddbf8196dbf8fd5f66f
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2018
ms.locfileid: "36925969"
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含每個 map-reduce 工作，會下推到 Hadoop 執行一部分的資料列[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]外部 Hadoop 資料表上的查詢。 每個 map-reduce 工作，代表其中一個查詢中的述詞。 這才會使用述詞下推查詢 Hadoop 的外部資料表上啟用時。  
  
|資料行名稱|資料類型|描述|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|這個外部 Hadoop 作業的識別碼。|與中的識別碼相同[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。|  
|step_index|**int**|此 Hadoop 作業是指查詢步驟索引。|相同中 step_index [sys.dm_pdw_request_steps &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)。|  
|operation_type|**nvarchar(255)**|描述外部的作業類型。|' 外部 Hadoop Operation'|  
|operation_name|**nvarchar(4000)**|Map-reduce 工作，作業識別碼。 這可由 Hadoop 之後傳回[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]提交工作。||  
|map_progress|**float**|已對應工作到目前為止使用的輸入資料的百分比。|浮點數字之間，以及包括 0 到 100 之間。|  
|reduce_progress|**int**|Reduce 作業已完成的百分比...|浮點數字之間，以及包括 0 到 100 之間。|  
  
## <a name="see-also"></a>另請參閱  
 [系統檢視表&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
