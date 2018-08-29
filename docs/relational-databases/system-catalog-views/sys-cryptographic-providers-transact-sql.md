---
title: sys.cryptographic_providers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- cryptographic_providers
- sys.cryptographic_providers
- sys.cryptographic_providers_TSQL
- cryptographic_providers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.cryptographic_providers catalog view
ms.assetid: 9da0da95-792e-48b4-9f60-47f0729c279c
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c7f0d08ce632e228ae93dcd9bfb578155897437
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43074055"
---
# <a name="syscryptographicproviders-transact-sql"></a>sys.cryptographic_providers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對每個註冊的密碼編譯提供者傳回一個資料列。  
    
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|密碼編譯提供者的識別碼。|  
|**name**|**sysname**|密碼編譯提供者的名稱。|  
|**guid**|**uniqueidentifier**|唯一的提供者 GUID。|  
|**version**|**nvarchar(50)**|以格式提供者版本 '*aa.bb.cccc.dd*'。|  
|**dll_path**|**nvarchar(512)**|實作可延伸金鑰管理 (EKM) 應用程式介面 (API) 的 DLL 路徑。|  
|**is_enabled**|**bit**|在伺服器上是否有啟用提供者。<br /><br /> 0 = 未啟用 (預設值)<br /><br /> 1 = 已啟用|  
  
## <a name="remarks"></a>備註  
 **Sys.cryptographic_providers**檢視是可以公開看到。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
  
