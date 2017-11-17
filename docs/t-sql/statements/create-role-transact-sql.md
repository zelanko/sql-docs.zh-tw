---
title: "建立角色 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ROLE
- DATABASE ROLE
- ROLE_TSQL
- DATABASE_ROLE_TSQL
- CREATE_ROLE_TSQL
- CREATE DATABASE ROLE
- ROLE
- CREATE_DATABASE_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], creating
- CREATE DATABASE ROLE statement
- roles [SQL Server], creating
- CREATE ROLE statement
ms.assetid: b0cd54ad-e81d-4d71-acec-8a6d7261ca08
caps.latest.revision: 54
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21e3cca3d07d7f53d646b5dd052fd40d0fa2cc1a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-role-transact-sql"></a>CREATE ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在目前資料庫中建立新的資料庫角色。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
## <a name="arguments"></a>引數  
 *role_name*  
 這是即將建立的角色名稱。  
  
 授權*owner_name*  
 這是要擁有新角色的資料庫使用者或角色。 如果未指定任何使用者，該角色便由執行 CREATE ROLE 的使用者所擁有。  
  
## <a name="remarks"></a>備註  
 角色是資料庫層級的安全性實體。 當您建立角色之後，請利用 GRANT、DENY 和 REVOKE，設定角色的資料庫層級權限。 若要將成員加入至資料庫角色，使用[ALTER ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md). 如需詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
 您可以在 sys.database_role_members 和 sys.database_principals 目錄檢視中，看到資料庫角色。  
  
 如需設計權限系統的資訊，請參閱 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 需要**CREATE ROLE**中的成員資格或資料庫上的權限**db_securityadmin**固定的資料庫角色。 當您使用**授權**選項時，下列權限也是必要的：  
  
-   若要指派角色擁有權給另一位使用者，則需要該使用者的 IMPERSONATE 權限。  
  
-   若要指派角色擁有權給另一個角色，則需要收件者角色中的成員資格，或該角色的 ALTER 權限。  
  
-   若要指派角色的擁有權給應用程式角色，則需要應用程式角色的 ALTER 權限。  
  
## <a name="examples"></a>範例  
下列範例都會使用 AdventureWorks 資料庫。   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>A. 建立資料庫使用者所擁有的資料庫角色  
 下列範例會建立使用者 `buyers` 所擁有的資料庫角色 `BenMiller`。  
  
```  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>B. 建立由固定資料庫角色所擁有的資料庫角色  
 下列範例會建立 `auditors` 固定資料庫角色所擁有的資料庫角色 `db_securityadmin`。  
  
```  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [更改角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  



