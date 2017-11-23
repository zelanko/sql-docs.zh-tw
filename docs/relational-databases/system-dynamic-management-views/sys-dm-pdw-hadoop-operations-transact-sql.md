---
title: "sys.dm_pdw_hadoop_operations (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 5d2337d4-e2c7-48de-9c26-cdc7e6eb5d55
caps.latest.revision: "5"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b735d4759d3164ae61da717ec18d54ab8661441
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwhadoopoperations-transact-sql"></a>sys.dm_pdw_hadoop_operations (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  包含每個 map-reduce 工作就會向下推送到 Hadoop 一部分執行的資料列[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]外部的 Hadoop 資料表上的查詢。 每個 map-reduce 工作，代表其中一個查詢中的述詞。 這只用查詢 Hadoop 的外部資料表啟用述詞下推。  
  
|資料行名稱|資料類型|Description|範圍|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar （32)**|這個外部的 Hadoop 作業的識別碼。|與 ID 中相同[sys.dm_pdw_exec_requests &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|這項 Hadoop 作業是指查詢步驟索引。|與中 step_index 相同[sys.dm_pdw_request_steps &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|operation_type|**nvarchar(255)**|描述外部作業類型。|' 外部 Hadoop Operation'|  
|operation_name|**nvarchar(4000)**|Map-reduce 工作作業識別碼。 這由之後 Hadoop[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]提交作業。||  
|map_progress|**float**|已對應作業到目前為止使用的輸入資料的百分比。|浮點數字之間，以及包含 0 到 100 之間。|  
|reduce_progress|**int**|減少作業已完成的百分比...|浮點數字之間，以及包含 0 到 100 之間。|  
  
## <a name="see-also"></a>請參閱＜  
 [系統檢視 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
