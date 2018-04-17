---
title: sys.security_policies (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- SYS.SECURITY_POLICIES_TSQL
- SECURITY_POLICIES_TSQL
- SYS.SECURITY_POLICIES
- SECURITY_POLICIES
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_policies catalog view
- security_policies catalog view
ms.assetid: 35362f5b-e601-4049-9e1d-c5307e823831
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6b588dcf21742dac41c9501bf165f7f9df04da62
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syssecuritypolicies-transact-sql"></a>sys.security_policies (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回資料庫中的每個安全性原則的資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|name|**sysname**|安全性原則的名稱，它在資料庫中是唯一的。|  
|object_id|**int**|安全性原則的識別碼。|  
|principal_id|**int**|註冊到資料庫之安全性原則的擁有者識別碼。 如果擁有者取決於結構描述，則為 NULL。|  
|schema_id|**int**|物件所在之結構描述的識別碼。|  
|parent_object_id|**int**|原則所屬之物件的識別碼。 必須是 0。|  
|型別|**vachar(2)**|必須是**SP**。|  
|type_desc|**nvarchar(60)**|**SECURITY_POLICY**。|  
|create_date|**datetime**|建立安全性原則的 UTC 日期。|  
|modify_date|**datetime**|上次修改安全性原則的 UTC 日期。|  
|is_ms_shipped|**bit**|一律為 false。|  
|is_enabled|**bit**|安全性原則規格狀態：<br /><br /> 0 = 已停用<br /><br /> 1 = 已啟用|  
|is_not_for_replication|**bit**|原則是利用 NOT FOR REPLICATION 選項來建立的。|  
|uses_database_collation|**bit**|使用與資料庫相同的定序。|  
|is_schemabinding_enabled|**bit**|安全性原則的 Schemabinding 狀態：<br /><br /> 0 或 NULL = 啟用<br /><br /> 1 = 已停用|  
  
## <a name="permissions"></a>Permissions  
 具有主體**ALTER ANY SECURITY POLICY**權限可以存取這份目錄檢視，以及任何人使用中的所有物件**VIEW DEFINITION**物件上。  
  
## <a name="see-also"></a>另請參閱  
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
