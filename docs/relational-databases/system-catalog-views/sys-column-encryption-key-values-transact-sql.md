---
description: 'sys.column_encryption_key_values (Transact-sql) '
title: sys.column_encryption_key_values (Transact-sql) |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da4a3997e724eb78d7c5742a03e5a2e15e1f74b5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482929"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>sys.column_encryption_key_values (Transact-sql) 
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回資料行加密金鑰的加密值 (Cek) 使用 [CREATE COLUMN ENCRYPTION key](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 或 [ALTER column Encryption key &#40;transact-sql&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 語句所建立的相關資訊。 每個資料列都代表 CEK 的值，以資料行主要金鑰加密 (CMK) 。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|資料庫中 CEK 的識別碼。|  
|**column_master_key_id**|**int**|用來加密 CEK 值的資料行主要金鑰的識別碼。|  
|**encrypted_value**|**varbinary(8000)**|使用 column_master_key_id 中指定的 CMK 加密的 CEK 值。|  
|**encryption_algorithm_name**|**sysname**|用來加密 CEK 值的演算法名稱。<br /><br /> 用來加密值之加密演算法的名稱。 系統提供者的演算法必須是  **RSA_OAEP**。|  
  
## <a name="permissions"></a>權限  
 需要 **VIEW ANY COLUMN ENCRYPTION KEY** 許可權。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [為具有安全記憶體保護區的 Always Encrypted 管理金鑰](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
