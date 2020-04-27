---
title: MSdbms_datatype_mapping （Transact-sql） |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67907540"
---
# <a name="msdbms_datatype_mapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype_mapping**資料表包含從源資料庫管理系統（DBMS）中的資料類型對應到目的地 DBMS 中的一或多個特定資料類型的允許資料類型對應。 此資料表會儲存在**msdb**資料庫中，並用於異質資料庫複寫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|識別每個唯一的資料類型對應。|  
|**map_id**|**int**|識別來源資料類型。|  
|**dest_datatype_id**|**int**|識別目的地資料類型。|  
|**dest_precision**|**bigint**|定義目的地資料類型的有效位數，其中 Null 值表示不使用有效位數，而 **-1**值表示使用源資料類型的有效位數。|  
|**dest_scale**|**int**|定義目的地資料類型的小數值，其中 Null 值表示不使用小數值，而 **-1**的值表示使用源資料類型的小數值。|  
|**dest_length**|**bigint**|定義目的地資料類型的長度，其中 Null 值表示不使用長度，而 **-1**的值表示使用源資料類型的長度。|  
|**dest_nullable**|**bit**|指出對應中的目的地資料行是否允許 NULL 值，其中 NULL 值表示不需要這個目的地。|  
|**dest_createparams**|**int**|用來描述每個資料類型所適用之長度、有效位數和小數位數組合的點陣圖，其中包括：<br /><br /> **0x1** = PRECISION。<br /><br /> **0x2** = SCALE。<br /><br /> **0x4** = 長度。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 發行者的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
