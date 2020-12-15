---
description: sys.cryptographic_providers (Transact-SQL)
title: sys.cryptographic_providers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f32f7ceea8a68a3ddf1693ae9f382ee066d51eb1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462839"
---
# <a name="syscryptographic_providers-transact-sql"></a>sys.cryptographic_providers (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  針對每個註冊的密碼編譯提供者傳回一個資料列。  
    
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|密碼編譯提供者的識別碼。|  
|**name**|**sysname**|密碼編譯提供者的名稱。|  
|**guid**|**uniqueidentifier**|唯一的提供者 GUID。|  
|**version**|**nvarchar(50)**|格式為 '*aa.bb.cccc.dd*' 之提供者的版本。|  
|**dll_path**|**nvarchar(512)**|實作可延伸金鑰管理 (EKM) 應用程式介面 (API) 的 DLL 路徑。|  
|**is_enabled**|**bit**|在伺服器上是否有啟用提供者。<br /><br /> 0 = 未啟用 (預設值)<br /><br /> 1 = 已啟用|  
  
## <a name="permissions"></a>權限  
 公用可以看到 **sys.cryptographic_providers** view。  
  
## <a name="see-also"></a>另請參閱  
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [可延伸金鑰管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)  
  
  
