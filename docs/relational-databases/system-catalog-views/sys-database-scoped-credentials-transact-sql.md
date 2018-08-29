---
title: sys.database_scoped_credentials (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bcc007a9c4dc35058052c2802907036f0ea78de1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43086120"
---
# <a name="sysdatabasescopedcredentials-transact-sql"></a>sys.database_scoped_credentials & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  傳回每個資料庫的一個資料列範圍在資料庫中的認證。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|資料庫範圍認證的識別碼。 是在資料庫中是唯一的。|  
|NAME|**sysname**|名稱的資料庫範圍認證。 是在資料庫中是唯一的。|  
|credential_identity|**nvarchar(4000)**|要使用之識別的名稱。 這通常是 Windows 使用者。 這不需要是唯一的。|  
|create_date|**datetime**|建立資料庫範圍認證的時間。|  
|modify_date|**datetime**|上次修改的資料庫範圍認證的時間。|  
|target_type|**nvarchar(100)**|類型的資料庫範圍認證。 傳回`NULL`資料庫範圍認證。|  
|target_id|**int**|資料庫範圍認證對應至物件的識別碼。 傳回 0，資料庫範圍認證|  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 `CONTROL` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [DROP DATABASE SCOPED CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
