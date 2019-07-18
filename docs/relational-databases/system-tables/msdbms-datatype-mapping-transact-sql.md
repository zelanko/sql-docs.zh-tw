---
title: MSdbms_datatype_mapping (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a1042bb3aa7b6113121693cc66440ebbf81ce1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907540"
---
# <a name="msdbmsdatatypemapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype_mapping**資料表包含資料類型對應的資料類型從來源資料庫管理系統 (DBMS) 中目的地 DBMS 中的一或多個特定資料類型。 這份資料表儲存在**msdb**資料庫，並使用異質資料庫複寫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|識別每個唯一的資料類型對應。|  
|**map_id**|**int**|識別來源資料類型。|  
|**dest_datatype_id**|**int**|識別目的地資料類型。|  
|**dest_precision**|**bigint**|定義目的地資料類型，其中 NULL 值表示不使用有效位數，精確度值，並針對 **-1**表示使用來源資料類型的有效位數。|  
|**dest_scale**|**int**|定義標尺的目的地資料類型，其中 NULL 值表示不使用 小數位數，而值為 **-1**表示使用來源資料類型的小數位數。|  
|**dest_length**|**bigint**|定義長度的目的地資料類型，其中 NULL 值表示不使用長度，而值為 **-1**表示使用來源資料類型的長度。|  
|**dest_nullable**|**bit**|指出對應中的目的地資料行是否允許 NULL 值，其中 NULL 值表示不需要這個目的地。|  
|**dest_createparams**|**int**|用來描述每個資料類型所適用之長度、有效位數和小數位數組合的點陣圖，其中包括：<br /><br /> **0x1** = PRECISION。<br /><br /> **0x2** = 小數位數。<br /><br /> **0x4** = 長度。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 「 Oracle 發行者 」 端的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
