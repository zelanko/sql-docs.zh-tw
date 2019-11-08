---
title: sys.databases column_encryption_key_values （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c5dc4f2dc42452560162d214844e2264cd0e5e9
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593809"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>sys.databases column_encryption_key_values （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對使用[CREATE column encryption key](../../t-sql/statements/create-column-encryption-key-transact-sql.md)或[ALTER column encryption key &#40;transact-sql&#41; ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)語句所建立的資料行加密金鑰（cek），傳回其加密值的相關資訊。 每個資料列都代表 CEK 的值，並使用資料行主要金鑰（CMK）進行加密。  
  
|資料行名稱|資料類型|說明|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|資料庫中 CEK 的識別碼。|  
|**column_master_key_id**|**int**|用來加密 CEK 值的資料行主要金鑰識別碼。|  
|**encrypted_value**|**varbinary(8000)**|使用 column_master_key_id 中指定的 CMK 加密的 CEK 值。|  
|**encryption_algorithm_name**|**sysname**|用來加密 CEK 值的演算法名稱。<br /><br /> 用來加密值之加密演算法的名稱。 系統提供者的演算法必須**RSA_OAEP**。|  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW ANY COLUMN ENCRYPTION KEY**許可權。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [使用 secure 記憶體保護區  的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)  
 [Always Encrypted  的金鑰管理總覽](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)  
 [使用安全記憶體保護區管理 Always Encrypted 的金鑰](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
