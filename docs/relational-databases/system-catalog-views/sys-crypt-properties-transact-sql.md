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
ms.openlocfilehash: 9655866d4fd2d6f98b38532f77f94bc12f16f9b4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68109486"
---
# <a name="syscrypt_properties-transact-sql"></a>sys.crypt_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對每一個與安全性實體相關聯的密碼編譯屬性，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|識別屬性所在的項目類別。<br /><br /> 1 = 物件或資料行<br /> 5 = 組件|  
|**class_desc**|**nvarchar(60)**|屬性所在項目類別的描述。<br /><br /> OBJECT_OR_COLUMN<br /> ASSEMBLY|  
|**major_id**|**int**|屬性所在項目的識別碼，根據類別加以解譯|  
|**thumbprint**|**varbinary(32)**|所用憑證或非對稱金鑰的 SHA-1 雜湊。|  
|**crypt_type**|**char （4）**|加密類型。<br /><br /> SPVC = 以憑證私密金鑰簽署<br /><br /> SPVA = 以非對稱式私密金鑰簽署<br /><br /> CPVC = 以憑證私密金鑰簽署的計數器簽章<br /><br /> CPVA = 以非對稱金鑰簽署的計數器簽章|  
|**crypt_type_desc**|**nvarchar(60)**|加密類型的描述。<br /><br /> SIGNATURE BY CERTIFICATE<br /><br /> SIGNATURE BY ASYMMETRIC KEY<br /><br /> COUNTER SIGNATURE BY CERTIFICATE<br /><br /> COUNTER SIGNATURE BY ASYMMETRIC KEY|  
|**crypt_property**|**varbinary(max)**|簽署或加密的位元。 針對已簽署的模組，這些是模組的簽章位。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性目錄檢視](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [安全性實體](../../relational-databases/security/securables.md)   
 [建立憑證 &#40;Transact-sql&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [建立對稱金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [建立非對稱金鑰 &#40;Transact-sql&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
