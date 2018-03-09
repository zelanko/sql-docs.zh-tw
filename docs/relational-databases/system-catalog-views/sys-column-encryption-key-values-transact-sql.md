---
title: "sys.column_encryption_key_values (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7bc9fa475e7e7fba6a8fac7bdb4e014742b6ad21
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnencryptionkeyvalues-transact-sql"></a>sys.column_encryption_key_values (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回加密值資訊的資料行加密金鑰 (Cek) 是以建立[CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)或[ALTER COLUMN ENCRYPTION KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)陳述式。 每個資料列代表 CEK，資料行主要金鑰 (CMK) 以加密值。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|在資料庫中 CEK 的識別碼。|  
|**column_master_key_id**|**int**|用來加密 CEK 值資料行主要金鑰的識別碼。|  
|**encrypted_value**|**varbinary （8000)**|CEK 加密的 CMK column_master_key_id 中指定的值。|  
|**encryption_algorithm_name**|**sysname**|用來加密 CEK 值演算法的名稱。<br /><br /> 用來加密值的加密演算法的名稱。 系統提供者的演算法必須是**RSA_OAEP**。|  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW ANY COLUMN ENCRYPTION KEY**權限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER 資料行加密金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [卸除資料行加密金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
