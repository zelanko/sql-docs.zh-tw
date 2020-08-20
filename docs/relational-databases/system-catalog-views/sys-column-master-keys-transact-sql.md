---
description: sys.column_master_keys (Transact-SQL)
title: sys. column_master_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a0192fd9a323e750a2fd8f635da93f4c4f549ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482135"
---
# <a name="syscolumn_master_keys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  針對使用 [CREATE MASTER key](../../t-sql/statements/create-column-master-key-transact-sql.md) 語句加入的每個資料庫主要金鑰，各傳回一個資料列。 每個資料列都代表單一資料行主要金鑰 (CMK) 。  
    
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK 的名稱。|  
|**column_master_key_id**|**int**|資料行主要金鑰的識別碼。|  
|**create_date**|**datetime**|建立資料行主要金鑰的日期。|  
|**modify_date**|**datetime**|上次修改資料行主要金鑰的日期。|  
|**key_store_provider_name**|**sysname**|包含 CMK 之資料行主要金鑰存放區的提供者名稱。 允許的值包括：<br /><br /> MSSQL_CERTIFICATE_STORE-如果資料行主要金鑰存放區為憑證存放區。<br /><br /> 如果資料行主要金鑰存放區是自訂類型，則為使用者定義值。|  
|**key_path**|**nvarchar(4000)**|金鑰的資料行主要金鑰存放區特定路徑。 路徑的格式取決於資料行主要金鑰存放區類型。 範例：<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 若為自訂資料行主要金鑰存放區，開發人員必須負責定義自訂資料行主要金鑰存放區的金鑰路徑。|  
|**allow_enclave_computations**|**bit**|表示資料行主要金鑰是否記憶體保護區啟用， (如果資料行加密金鑰（使用此主要金鑰加密）可以用於伺服器端安全記憶體保護區) 內的計算。 如需詳細資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。|  
|**簽章**|**varbinary(max)**|使用**key_path**所參考的資料行主要金鑰所產生**key_path**和**allow_enclave_computations**的數位簽章。|


  
## <a name="permissions"></a>權限  
 需要 **VIEW ANY COLUMN MASTER KEY** 許可權。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;建立資料行主要金鑰 ](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted 的金鑰管理總覽](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [為具有安全記憶體保護區的 Always Encrypted 管理金鑰](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
 
  
  
