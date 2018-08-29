---
title: sys.credentials (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1931d0cb4a11f0fd1a7ddfb1a83a2bcebb0b94d9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43070191"
---
# <a name="syscredentials-transact-sql"></a>sys.credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  傳回一個資料列的每個伺服器層級的認證。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|認證的識別碼。 這在伺服器中是唯一的。|  
|NAME|**sysname**|認證的名稱。 這在伺服器中是唯一的。|  
|credential_identity|**nvarchar(4000)**|要使用之識別的名稱。 這通常是 Windows 使用者。 這不需要是唯一的。|  
|create_date|**datetime**|建立認證的時間。|  
|modify_date|**datetime**|上次修改認證的時間。|  
|target_type|**nvarchar(100)**|認證的類型。 針對傳統的認證傳回 NULL，針對對應至密碼編譯提供者的認證傳回 CRYPTOGRAPHIC PROVIDER。 如需有關外部金鑰管理提供者的詳細資訊，請參閱 < [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。|  
|target_id|**int**|此認證對應之物件的識別碼。 針對傳統的認證傳回 0，針對對應至密碼編譯提供者的認證傳回非 0 值。 如需有關外部金鑰管理提供者的詳細資訊，請參閱 < [Extensible Key Management &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。|  

## <a name="remarks"></a>備註  
資料庫層級的認證，請參閱[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)。
  
## <a name="permissions"></a>Permissions  
 需要`VIEW ANY DEFINITION`權限或`ALTER ANY CREDENTIAL`權限。 此外，不應拒絕主體`VIEW ANY DEFINITION`權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [認證 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)  
  
  
