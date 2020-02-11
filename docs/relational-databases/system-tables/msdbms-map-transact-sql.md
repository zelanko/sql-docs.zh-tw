---
title: MSdbms_map （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: fffa30d0e252392c41cee34c1875b12b5b7a53b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907494"
---
# <a name="msdbms_map-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_map**資料表包含源資料類型資訊，以及來源和目的地 DBMS 配對的預設目的地資料類型資訊的連結。 此資料表會儲存在**msdb**資料庫中，並用於進行異類發行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|唯一識別資料類型對應。|  
|**src_dbms_id**|**int**|藉由在[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)資料表中指定其**dbms_id** ，來識別來源 DBMS。|  
|**dest_dbms_id**|**int**|藉由在[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)資料表中指定其**dbms_id** ，來識別目的地 DBMS。|  
|**src_datatype_id**|**int**|識別源資料類型之[MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md)資料表的**datatype_id** 。|  
|**src_len_min**|**Bigint**|來源 DBMS 的資料類型最小長度，如果其值為 NULL，表示不使用長度。|  
|**src_len_max**|**Bigint**|來源 DBMS 的資料類型最大長度，如果其值為 NULL，表示不使用長度。|  
|**src_prec_min**|**Bigint**|來源 DBMS 的資料類型最小有效位數，如果其值為 NULL，表示不使用有效位數。|  
|**src_prec_max**|**Bigint**|來源 DBMS 的資料類型最大有效位數，如果其值為 NULL，表示不使用有效位數。|  
|**src_scale_min**|**int**|來源 DBMS 的資料類型最小小數位數，如果其值為 NULL，表示不使用小數位數。|  
|**src_scale_max**|**int**|來源 DBMS 的資料類型最大小數位數，如果其值為 NULL，表示不使用小數位數。|  
|**src_nullable**|**bit**|指出對應中的目的地資料行是否允許 NULL 值，其中 NULL 值表示不需要這個目的地。|  
|**default_datatype_mapping_id**|**int**|藉由在資料表[MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)中指定其**map_id** ，識別預設的資料類型對應。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 Oracle 發行者的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
