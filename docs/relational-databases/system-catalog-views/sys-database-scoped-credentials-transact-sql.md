---
title: sys.databases database_scoped_credentials （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.database_scoped_credentials
- sys.database_scoped_credentials_TSQL
- database_scoped_credentials
- database_scoped_credentials_TSQL
helpviewer_keywords:
- sys.database_scoped_credentials catalog view
ms.assetid: 68e8aa6b-bcdc-42aa-93d8-d498f724c188
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 13d5138d5ebc318947d010e60d6d5cc175d89c62
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396186"
---
# <a name="sysdatabase_scoped_credentials-transact-sql"></a>sys.databases database_scoped_credentials （Transact-sql）
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  針對資料庫中的每個資料庫範圍認證，各傳回一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|資料庫範圍認證的名稱。 在資料庫中是唯一的。|  
|credential_id|**int**|資料庫範圍認證的識別碼。 在資料庫中是唯一的。|  
|principal_id|**int**|擁有金鑰的資料庫主體識別碼。|  
|credential_identity|**nvarchar(4000)**|要使用之識別的名稱。 這通常是 Windows 使用者。 這不需要是唯一的。|  
|create_date|**datetime**|建立資料庫範圍認證的時間。|  
|modify_date|**datetime**|上次修改資料庫範圍認證的時間。|  
|target_type|**Nvarchar （100）**|資料庫範圍認證的類型。 傳回 `NULL` 資料庫範圍認證的。|  
|target_id|**int**|資料庫範圍認證所對應之物件的識別碼。 針對資料庫範圍認證傳回0|  
  
## <a name="permissions"></a>權限  
 需要資料庫的 `CONTROL` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [建立資料庫範圍認證 &#40;Transact-sql&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE 範圍認證 &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [卸載資料庫範圍認證 &#40;Transact-sql&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
