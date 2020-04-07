---
title: sys. 認證(轉用 SQL) |微軟文件
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.credentials
- sys.credentials_TSQL
- credentials_TSQL
- credentials
dev_langs:
- TSQL
helpviewer_keywords:
- sys.credentials catalog view
ms.assetid: ea48cf80-904a-4273-a950-6d35b1b0a1b6
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f87378897256f8b4fae26b30263577bedede6175
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2020
ms.locfileid: "80752886"
---
# <a name="syscredentials-transact-sql"></a>sys.credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdbmi-asdw-pdw-md.md)]

  為每個伺服器級憑據返回一行。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|認證的識別碼。 這在伺服器中是唯一的。|  
|NAME|**sysname**|認證的名稱。 這在伺服器中是唯一的。|  
|credential_identity|**nvarchar(4000)**|要使用之識別的名稱。 這通常是 Windows 使用者。 這不需要是唯一的。|  
|create_date|**datetime**|建立認證的時間。|  
|modify_date|**datetime**|上次修改認證的時間。|  
|target_type|**恩瓦爾查爾 (100)**|認證的類型。 針對傳統的認證傳回 NULL，針對對應至密碼編譯提供者的認證傳回 CRYPTOGRAPHIC PROVIDER。 有關外部金鑰管理提供程式的詳細資訊,請參閱[可擴充金鑰管理&#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。|  
|target_id|**int**|此認證對應之物件的識別碼。 針對傳統的認證傳回 0，針對對應至密碼編譯提供者的認證傳回非 0 值。 有關外部金鑰管理提供程式的詳細資訊,請參閱[可擴充金鑰管理&#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。|  

## <a name="remarks"></a>備註  
有關資料庫級認證,請參閱[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)。
  
## <a name="permissions"></a>權限  
 需要許可權`VIEW ANY DEFINITION``ALTER ANY CREDENTIAL`或許可權。 此外,不得拒絕`VIEW ANY DEFINITION`委託人的許可權。  
  
## <a name="see-also"></a>另請參閱  
 [系統database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [認證&#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [安全目錄檢視&#40;交易-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
