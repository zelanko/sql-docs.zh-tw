---
title: sys.databases security_policies （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d6eec5c523e2bdd321af145f19d0b5e7e7cba39b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135305"
---
# <a name="syssecurity_policies-transact-sql"></a>sys.databases security_policies （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  針對資料庫中的每個安全性原則，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|安全性原則的名稱，它在資料庫中是唯一的。|  
|object_id|**int**|安全性原則的識別碼。|  
|principal_id|**int**|註冊到資料庫之安全性原則的擁有者識別碼。 如果擁有者取決於結構描述，則為 NULL。|  
|schema_id|**int**|物件所在之結構描述的識別碼。|  
|parent_object_id|**int**|原則所屬之物件的識別碼。 必須是 0。|  
|type|**vachar （2）**|必須是**SP**。|  
|type_desc|**Nvarchar （60）**|**SECURITY_POLICY**。|  
|create_date|**datetime**|建立安全性原則的 UTC 日期。|  
|modify_date|**datetime**|上次修改安全性原則的 UTC 日期。|  
|is_ms_shipped|**bit**|一律為 false。|  
|is_enabled|**bit**|安全性原則規格狀態：<br /><br /> 0 = 已停用<br /><br /> 1 = 已啟用|  
|is_not_for_replication|**bit**|原則是利用 NOT FOR REPLICATION 選項來建立的。|  
|uses_database_collation|**bit**|使用與資料庫相同的定序。|  
|is_schemabinding_enabled|**bit**|Schemabinding 安全性原則的狀態：<br /><br /> 0或 Null = 已啟用<br /><br /> 1 = 已停用|  
  
## <a name="permissions"></a>權限  
 具有**ALTER ANY SECURITY POLICY**許可權的主體可存取此目錄檢視中的所有物件，以及具有物件之**view DEFINITION**的任何人。  
  
## <a name="see-also"></a>另請參閱  
 [資料列層級安全性](../../relational-databases/security/row-level-security.md)   
 [security_predicates &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [&#40;Transact-sql&#41;的安全性目錄檢視](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
