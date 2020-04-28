---
title: sys.databases database_credentials （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_credentials
- sys.database_credentials_TSQL
- database_credentials
- database_credentials_TSQL
helpviewer_keywords:
- sys.database_credentials catalog view
ms.assetid: 796322df-e62a-45bf-b519-89e1d521abce
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2521d9543c71d9dee298fbb58518163fd45fbfdc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67999523"
---
# <a name="sysdatabase_credentials-transact-sql"></a>sys.databases database_credentials （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  針對資料庫中的每個資料庫範圍認證，各傳回一個資料列。  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys. database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) 。    
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|credential_id|**int**|資料庫範圍認證的識別碼。 在資料庫中是唯一的。|  
|NAME|**sysname**|資料庫範圍認證的名稱。 在資料庫中是唯一的。|  
|credential_identity|**nvarchar(4000)**|要使用之識別的名稱。 這通常是 Windows 使用者。 這不需要是唯一的。|  
|create_date|**datetime**|建立資料庫範圍認證的時間。|  
|modify_date|**datetime**|上次修改資料庫範圍認證的時間。|  
|target_type|**Nvarchar （100）**|資料庫範圍認證的類型。 針對資料庫範圍認證傳回 Null。|  
|target_id|**int**|資料庫範圍認證所對應之物件的識別碼。 針對資料庫範圍認證傳回0|  
  
## <a name="permissions"></a>權限  
 需要資料庫的 `CONTROL` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40;資料庫引擎&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [建立資料庫範圍認證 &#40;Transact-sql&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE 範圍認證 &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [卸載資料庫範圍認證 &#40;Transact-sql&#41;](../../t-sql/statements/drop-database-scoped-credential-transact-sql.md)   
 [&#40;Transact-sql&#41;建立認證](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  
