---
title: sys.column_master_keys (TRANSACT-SQL) |Microsoft 文件
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
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c514b239547c943adbd8cedf1d7295e1c7ca07c2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回一個資料列使用新增的每個資料庫主要金鑰[CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)陳述式。 每個資料列都代表單一資料行主要金鑰 (CMK)。  
    
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK 的名稱。|  
|**column_master_key_id**|**int**|資料行主要金鑰的識別碼。|  
|**create_date**|**datetime**|資料行主要金鑰的建立日期。|  
|**modify_date**|**datetime**|上次修改資料行主要金鑰的日期。|  
|**key_store_provider_name**|**sysname**|包含 CMK 的資料行主要金鑰存放區提供者名稱。 允許的值如下：<br /><br /> MSSQL_CERTIFICATE_STORE – 如果資料行主要金鑰存放區是憑證存放區。<br /><br /> 使用者定義值，如果資料行主要金鑰存放區的自訂類型。|  
|**key_path**|**nvarchar(4000)**|索引鍵資料行主要金鑰儲存特定路徑。 路徑的格式取決於資料行主要金鑰存放區型別。 範例：<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 自訂資料行主要金鑰存放區中，開發人員負責定義的機碼路徑就是自訂的資料行主要金鑰存放區。|  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW ANY COLUMN MASTER KEY**權限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
