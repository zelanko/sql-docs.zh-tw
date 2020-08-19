---
description: sysdatatypemappings (Transact-SQL)
title: sysdatatypemappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
author: stevestein
ms.author: sstein
ms.openlocfilehash: ad4a6df1ae2dbdd418e133053330095a389bdf24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427530"
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysdatatypemappings** view 可用來顯示 SQL Server 資料類型，以及 (DBMS) 之非 SQL Server 資料庫管理系統的資料類型之間的對應。 這個視圖會儲存在 **msdb** 資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|資料類型對應的識別碼。|  
|**source_dbms**|**sysname**|指出資料類型對應的來源 DBMS 名稱，它可以是下列值之一：<br /><br /> **MSSQLSERVER** = 來源是 SQL Server 資料庫。<br /><br /> **Oracle** = 來源是 oracle 資料庫。|  
|**source_version**|**sysname**|指出來源 DBMS 的產品版本。|  
|**source_type**|**sysname**|指出來源 DBMS 中所列出的資料類型。|  
|**source_length_min**|**bigint**|來源 DBMS 的資料類型最小長度，如果其值為 NULL，表示不使用長度。|  
|**source_length_max**|**bigint**|來源 DBMS 的資料類型最大長度，如果其值為 NULL，表示不使用長度。|  
|**source_precision_min**|**bigint**|來源 DBMS 的資料類型最小有效位數，如果其值為 NULL，表示不使用有效位數。|  
|**source_precision_max**|**bigint**|來源 DBMS 的資料類型最大有效位數，如果其值為 NULL，表示不使用有效位數。|  
|**source_scale_min**|**int**|來源 DBMS 的資料類型最小小數位數，如果其值為 NULL，表示不使用小數位數。|  
|**source_scale_max**|**int**|來源 DBMS 的資料類型最大小數位數，如果其值為 NULL，表示不使用小數位數。|  
|**source_nullable**|**bit**|指出目的地資料類型是否支援 Null 值。|  
|**source_createparams**|**int**|僅供內部使用。|  
|**destination_dbms**|**sysname**|指出目的地 DBMS 的名稱，它可以是下列值之一：<br /><br /> **MSSQLSERVER** = 目的地是 SQL Server 資料庫。<br /><br /> **Oracle** = 目的地是 oracle 資料庫。<br /><br /> **DB2** = 目的地是 IBM DB2 資料庫。<br /><br /> **Sybase** = 目的地是 sybase 資料庫。|  
|**destination_version**|**sysname**|目的地 DBMS 的產品版本。|  
|**destination_type**|**sysname**|目的地 DBMS 的資料類型。|  
|**destination_length**|**bigint**|目的地 DBMS 的資料類型長度。|  
|**destination_precision**|**bigint**|目的地 DBMS 之資料類型的有效位數。|  
|**destination_scale**|**int**|目的地 DBMS 之資料類型的小數位數。|  
|**destination_nullable**|**bit**|指出目的地 DBMS 中的資料類型是否支援 Null 值。|  
|**destination_createparams**|**int**|僅供內部使用。|  
|**資料遺失**|**bit**|指出在來源和目的地 DBMS 的資料類型之間對應時，是否遺失資料。|  
|**is_default**|**bit**|指出是否會依預設使用資料類型對應。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [&#40;Transact-sql&#41;的複寫視圖 ](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
