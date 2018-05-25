---
title: sys.dm_cryptographic_provider_properties (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_properties_TSQL
- sys.dm_cryptographic_provider_properties
- sys.dm_cryptographic_provider_properties_TSQL
- dm_cryptographic_provider_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_properties dynamic management view
ms.assetid: 024b0095-6766-4189-a39a-d316c5ec2874
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: af1e68502ad7be83a8cfa8f3477420d7336e5f43
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmcryptographicproviderproperties-transact-sql"></a>sys.dm_cryptographic_provider_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關已註冊之密碼編譯提供者的資訊。  
  
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|provider_id|**int**|密碼編譯提供者的識別碼。|  
|guid|**uniqueidentifier**|唯一的提供者 GUID。|  
|provider_version|**nvarchar(256)**|以格式提供者版本 '*aa.bb.cccc.dd*'。|  
|sqlcrypt_version|**nvarchar(256)**|主要版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]格式的密碼編譯 API '*aa.bb.cccc.dd*'。|  
|friendly_name|**nvarchar(2048)**|提供者所提供的名稱。|  
|authentication_type|**nvarchar(256)**|WINDOWS、BASIC 或 OTHER。|  
|symmetric_key_support|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
|symmetric_key_export|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
|symmetric_key_import|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
|symmetric_key_persistance|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
|asymmetric_key_support|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
|asymmetric_key_export|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
|symmetric_key_import|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
|symmetric_key_persistance|**tinyint**|0 (不支援)<br /><br /> 1 (支援)|  
  
## <a name="remarks"></a>備註  
 sys.dm_cryptographic_provider_properties 檢視表會公開讓人看到。  
  
## <a name="see-also"></a>另請參閱  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [安全性相關的動態管理檢視和函數 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
