---
title: "DROP DATABASE SCOPED CREDENTIAL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP DATABASE SCOPED CREDENTIAL
- DROP_DATABASE_SCOPED_CREDENTIAL_TSQL
helpviewer_keywords:
- DROP DATABASE SCOPED CREDENTIAL statement
- credential [SQL Server], DROP DATABASE SCOPED CREDENTIAL statement
ms.assetid: 319d59f4-fa82-47ca-869b-3a9cd52900b0
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3768e6b95fb991b784c7c4f29c70599970ac1453
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-database-scoped-credential-transact-sql"></a>DROP DATABASE SCOPED CREDENTIAL (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  從伺服器中移除的資料庫範圍認證。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP DATABASE SCOPED CREDENTIAL credential_name  
```  
  
## <a name="arguments"></a>引數  
 *credential_name*  
 是要從伺服器移除的資料庫範圍認證的名稱。  
  
## <a name="remarks"></a>備註  
 若要卸除但不卸除資料庫範圍認證本身相關聯的資料庫範圍認證的密碼，請使用[ALTER CREDENTIAL](../../t-sql/statements/alter-credential-transact-sql.md)。  
  
 資料庫範圍認證的相關資訊會顯示在[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 需要`ALTER`權限的認證。  
  
## <a name="examples"></a>範例  
 下列範例會移除資料庫範圍認證呼叫`SalesAccess`。  
  
```tsql  
DROP DATABASE SCOPED CREDENTIAL AppCred;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [認證 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [建立 DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)   
 [ALTER DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-credential-transact-sql.md)   
 [sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  
  

