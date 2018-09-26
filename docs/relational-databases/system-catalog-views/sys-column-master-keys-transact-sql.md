---
title: sys.column_master_keys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e683a88fb9490a7041ac02edc02a8ba2f63b1382
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713540"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回一個資料列，使用新增的每個資料庫主要金鑰[CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)陳述式。 每個資料列都代表單一資料行主要金鑰 (CMK)。  
    
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|CMK 的名稱。|  
|**column_master_key_id**|**int**|資料行主要金鑰的識別碼。|  
|**create_date**|**datetime**|資料行主要金鑰的建立日期。|  
|**modify_date**|**datetime**|上次修改資料行主要金鑰的日期。|  
|**key_store_provider_name**|**sysname**|包含 CMK 的資料行主要金鑰存放區提供者名稱。 允許的值為：<br /><br /> MSSQL_CERTIFICATE_STORE – 如果資料行主要金鑰存放區是憑證存放區。<br /><br /> 使用者定義的值，如果資料行主要金鑰存放區的自訂型別。|  
|**key_path**|**nvarchar(4000)**|索引鍵資料行主要金鑰存放區特定路徑。 路徑的格式取決於資料行主要金鑰存放區類型。 範例<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> 自訂資料行主要金鑰存放區中，開發人員會負責定義哪些金鑰的路徑是自訂資料行主要金鑰存放區。|  
|**allow_enclave_computations**|**bit**|指出資料行主要金鑰是否啟用 enclave 的 （如果使用這個主要金鑰加密的資料行加密金鑰可用於在伺服器端的安全 enclaves 計算）。 如需詳細資訊，請參閱 < [Always Encrypted with 安全 enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。|  
|**signature**|**varbinary(max)**|數位簽章**key_path**並**allow_enclave_computations**，使用資料行主要金鑰所產生，所參考**key_path**。|


  
## <a name="permissions"></a>Permissions  
 需要**VIEW ANY COLUMN MASTER KEY**權限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
