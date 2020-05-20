---
title: sys.databases key_encryptions （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e1e7b6568b99b8a3af83e72b39036fc36faaa34c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82825170"
---
# <a name="syskey_encryptions-transact-sql"></a>sys.key_encryptions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對使用 CREATE SYMMETRIC KEY 陳述式的 ENCRYPTION BY 子句指定的每一個對稱金鑰加密，各傳回一個資料列。  

  
|資料行名稱|資料類型|描述|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|加密金鑰的識別碼。|  
|**特徵**|**varbinary(32)**|用來加密金鑰的憑證 SHA-1 雜湊，或用來加密金鑰的對稱金鑰 GUID。|  
|**crypt_type**|**char （4）**|加密的類型：<br /><br /> ESKS = 由對稱金鑰加密<br /><br /> ESKP、ESP2 或 ESP3 = 以密碼加密<br /><br /> EPUC = 由憑證加密<br /><br /> EPUA = 由非對稱金鑰加密<br /><br /> ESKM = 由主要金鑰加密|  
|**crypt_type_desc**|**nvarchar(60)**|加密類型的描述：<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />（從開始 [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] ，包含可供 CSS 使用的版本號碼）。<br /><br /> ENCRYPTION BY CERTIFICATE <br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> 注意： Windows DPAPI 是用來保護服務主要金鑰。|  
|**crypt_property**|**varbinary(max)**|簽署或加密的位元。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的目錄檢視](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的安全性目錄檢視](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
