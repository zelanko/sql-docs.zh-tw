---
title: MSdbms_map (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
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
manager: craigg
ms.openlocfilehash: a718cd7130e13ed5e9afddadddf7c1b5e3ee0ccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832956"
---
# <a name="msdbmsmap-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_map**資料表包含來源資料類型資訊，以及來源和目的地 DBMS 配對預設目的地資料類型資訊的連結。 這份資料表儲存在**msdb**資料庫，並使用於異質性發行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**msdbms_datatype_mapping**|**int**|唯一識別資料類型對應。|  
|**src_dbms_id**|**int**|識別來源 DBMS 藉由指定其**msdbms**中[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)資料表。|  
|**dest_dbms_id**|**int**|識別目的地 DBMS 藉由指定其**msdbms**中[MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)資料表。|  
|**src_datatype_id**|**int**|識別**msdbms_datatype**從[MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md)來源資料類型的資料表。|  
|**src_len_min**|**bigint**|來源 DBMS 的資料類型最小長度，如果其值為 NULL，表示不使用長度。|  
|**src_len_max**|**bigint**|來源 DBMS 的資料類型最大長度，如果其值為 NULL，表示不使用長度。|  
|**src_prec_min**|**bigint**|來源 DBMS 的資料類型最小有效位數，如果其值為 NULL，表示不使用有效位數。|  
|**src_prec_max**|**bigint**|來源 DBMS 的資料類型最大有效位數，如果其值為 NULL，表示不使用有效位數。|  
|**src_scale_min**|**int**|來源 DBMS 的資料類型最小小數位數，如果其值為 NULL，表示不使用小數位數。|  
|**src_scale_max**|**int**|來源 DBMS 的資料類型最大小數位數，如果其值為 NULL，表示不使用小數位數。|  
|**src_nullable**|**bit**|指出對應中的目的地資料行是否允許 NULL 值，其中 NULL 值表示不需要這個目的地。|  
|**default_datatype_mapping_id**|**int**|識別預設資料類型對應，藉由指定其**msdbms_datatype_mapping**資料表中[MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 「 Oracle 發行者 」 端的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
