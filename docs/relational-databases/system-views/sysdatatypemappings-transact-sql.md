---
title: sysdatatypemappings (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysdatatypemappings
- sysdatatypemappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdatatypemappings view
ms.assetid: 5dfafb70-3e3d-4465-b293-1acff1f855b6
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6bf0df894d81eaa0688462a813578ab827c47b7f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatatypemappings-transact-sql"></a>sysdatatypemappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysdatatypemappings**檢視用來顯示 SQL Server 資料類型和資料類型的非 SQL Server 資料庫管理系統 (DBMS) 之間的對應。 這份檢視儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**mapping_id**|**int**|資料類型對應的識別碼。|  
|**source_dbms**|**sysname**|指出資料類型對應的來源 DBMS 名稱，它可以是下列值之一：<br /><br /> **MSSQLSERVER** = 來源是 SQL Server 資料庫。<br /><br /> **ORACLE** = 來源是 Oracle 資料庫。|  
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
|**destination_dbms**|**sysname**|指出目的地 DBMS 的名稱，它可以是下列值之一：<br /><br /> **MSSQLSERVER** = 目的地是 SQL Server 資料庫。<br /><br /> **ORACLE** = 目的地是一個 Oracle 資料庫。<br /><br /> **DB2** = 目的地是 IBM DB2 資料庫。<br /><br /> **SYBASE** = 目的地是一個 Sybase 資料庫。|  
|**destination_version**|**sysname**|目的地 DBMS 的產品版本。|  
|**destination_type**|**sysname**|目的地 DBMS 的資料類型。|  
|**destination_length**|**bigint**|目的地 DBMS 的資料類型長度。|  
|**destination_precision**|**bigint**|目的地 DBMS 之資料類型的有效位數。|  
|**destination_scale**|**int**|目的地 DBMS 之資料類型的小數位數。|  
|**destination_nullable**|**bit**|指出目的地 DBMS 中的資料類型是否支援 Null 值。|  
|**destination_createparams**|**int**|僅供內部使用。|  
|**dataloss**|**bit**|指出在來源和目的地 DBMS 的資料類型之間對應時，是否遺失資料。|  
|**is_default**|**bit**|指出是否會依預設使用資料類型對應。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helpdatatypemap &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)  
  
  
