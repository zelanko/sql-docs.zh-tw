---
title: "sysmergesubsetfilters (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmergesubsetfilters
- sysmergesubsetfilters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergesubsetfilters system table
ms.assetid: f91d1c6c-3132-47f6-926c-88f56848cafe
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66ef85eacefa716b50e3af7e125e877116185a64
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergesubsetfilters-transact-sql"></a>sysmergesubsetfilters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含資料分割發行項的聯結篩選資訊。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**filtername**|**sysname**|用來建立發行項的篩選名稱。|  
|**join_filterid**|**int**|代表聯結篩選的物件識別碼。|  
|**pubid**|**uniqueidentifier**|發行集的識別碼。|  
|**artid**|**uniqueidentifier**|發行項的識別碼。|  
|**art_nickname**|**int**|發行項的暱稱。|  
|**join_articlename**|**sysname**|要加以聯結以便判斷資料列是否屬於它的資料表名稱。|  
|**join_nickname**|**int**|要加以聯結以便判斷資料列是否屬於它的資料表暱稱。|  
|**join_unique_key**|**int**|表示唯一索引鍵的聯結**join_tablename**:<br /><br /> 0 = 不是唯一索引鍵。<br /><br /> 1 = 唯一索引鍵。|  
|**expand_proc**|**sysname**|合併代理程式用來識別需要從訂閱者中傳送或移除之資料列的預存程序名稱。|  
|**join_filterclause**|**nvarchar （1000)**|用於聯結的篩選子句。|  
|**filter_type**|**tinyint**|指定篩選類型，它可以是下列項目之一：<br /><br /> 1 = 聯結篩選。<br /><br /> 2 = 邏輯記錄連結。<br /><br /> 3 = 聯結篩選和邏輯記錄連結。|  
  
## <a name="see-also"></a>請參閱＜  
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
