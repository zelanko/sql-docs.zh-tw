---
title: sys.databases column_encryption_keys （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_encryption_keys
- column_encryption_keys_TSQL
- sys.column_encryption_keys_TSQL
- column_encryption_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_keys catalog view
ms.assetid: 43980dd8-b9b1-4869-a304-2c183ae8977d
author: jaszymas
ms.author: jaszymas
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4cd6b4a4cb8eeed0dd0a2a78adc2d39c6a2e895d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73593723"
---
# <a name="syscolumn_encryption_keys--transact-sql"></a>sys.databases column_encryption_keys （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md)]

  傳回使用[CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)語句所建立之資料行加密金鑰（cek）的相關資訊。 每個資料列都代表 CEK。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK 的名稱。|  
|**column_encryption_key_id**|**int**|CEK 的識別碼。|  
|**create_date**|**datetime**|CEK 的建立日期。|  
|**modify_date**|**datetime**|上次修改 CEK 的日期。|  
  
## <a name="permissions"></a>權限  
 需要**VIEW ANY COLUMN ENCRYPTION KEY**許可權。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料行加密金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [改變數據行加密金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [卸載資料行加密金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [建立資料行主要金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [&#40;Transact-sql&#41;的安全性目錄檢視](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [使用安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 的金鑰管理總覽](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [為具有安全記憶體保護區的 Always Encrypted 管理金鑰](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)    

  
  
