---
title: sys.databases crypt_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- crypt_properties
- crypt_properties_TSQL
- sys.crypt_properties_TSQL
- sys.crypt_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.crypt_properties catalog view
ms.assetid: d5684f5a-30b1-418e-ae4d-ab040db9257e
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5a4c03687f6adac3f67f3e6aa231c384a6d5e009
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725798"
---
# <a name="syscrypt_properties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對每一個與安全性實體相關聯的密碼編譯屬性，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|識別屬性所在的項目類別。<br /><br /> 1 = 物件或資料行<br /> 5 = 組件|  
|**class_desc**|**nvarchar(60)**|屬性所在項目類別的描述。<br /><br /> OBJECT_OR_COLUMN<br /> ASSEMBLY|  
|**major_id**|**int**|屬性所在項目的識別碼，根據類別加以解譯|  
|**特徵**|**varbinary(32)**|所用憑證或非對稱金鑰的 SHA-1 雜湊。|  
|**crypt_type**|**char （4）**|加密類型。<br /><br /> SPVC = 以憑證私密金鑰簽署<br /><br /> SPVA = 以非對稱式私密金鑰簽署<br /><br /> CPVC = 以憑證私密金鑰簽署的計數器簽章<br /><br /> CPVA = 以非對稱金鑰簽署的計數器簽章|  
|**crypt_type_desc**|**nvarchar(60)**|加密類型的描述。<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> COUNTER SIGNATURE BY CERTIFICATE<br /><br /> COUNTER SIGNATURE BY ASYMMETRIC KEY|  
|**crypt_property**|**varbinary(max)**|簽署或加密的位元。 針對已簽署的模組，這些是模組的簽章位。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性目錄檢視](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [安全性實體](../../relational-databases/security/securables.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [建立對稱金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [建立非對稱金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
