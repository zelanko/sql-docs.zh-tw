---
description: CREATE ROLE (Transact-SQL)
title: CREATE ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e0ca6f481b84cfd1453359e3b77d47bb5a6b52b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458775"
---
# <a name="create-role-transact-sql"></a>CREATE ROLE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  在目前資料庫中建立新的資料庫角色。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql  
CREATE ROLE role_name [ AUTHORIZATION owner_name ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *role_name*  
 這是即將建立的角色名稱。  
  
 AUTHORIZATION *owner_name*  
 這是要擁有新角色的資料庫使用者或角色。 如果未指定任何使用者，該角色便由執行 CREATE ROLE 的使用者所擁有。 角色的擁有者，或是任何擁有角色的成員都可以新增或移除角色成員。
  
## <a name="remarks"></a>備註  
 角色是資料庫層級的安全性實體。 當您建立角色之後，請利用 GRANT、DENY 和 REVOKE，設定角色的資料庫層級權限。 若要在資料庫角色中新增成員，請使用 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)。 如需詳細資訊，請參閱[資料庫層級角色](../../relational-databases/security/authentication-access/database-level-roles.md)。  
  
 您可以在 sys.database_role_members 和 sys.database_principals 目錄檢視中，看到資料庫角色。  
  
 如需設計權限系統的資訊，請參閱 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>權限  
 需要資料庫的 **CREATE ROLE** 權限，或是 **db_securityadmin** 固定資料庫角色的成員資格。 當您使用 **AUTHORIZATION** 選項時，也必須具備下列權限：  
  
-   若要指派角色擁有權給另一位使用者，則需要該使用者的 IMPERSONATE 權限。  
  
-   若要指派角色擁有權給另一個角色，則需要收件者角色中的成員資格，或該角色的 ALTER 權限。  
  
-   若要指派角色的擁有權給應用程式角色，則需要應用程式角色的 ALTER 權限。  
  
## <a name="examples"></a>範例  
下列範例使用 AdventureWorks 資料庫。   

### <a name="a-creating-a-database-role-that-is-owned-by-a-database-user"></a>A. 建立資料庫使用者所擁有的資料庫角色  
 下列範例會建立使用者 `buyers` 所擁有的資料庫角色 `BenMiller`。  
  
```sql  
CREATE ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-database-role-that-is-owned-by-a-fixed-database-role"></a>B. 建立由固定資料庫角色所擁有的資料庫角色  
 下列範例會建立 `auditors` 固定資料庫角色所擁有的資料庫角色 `db_securityadmin`。  
  
```sql  
CREATE ROLE auditors AUTHORIZATION db_securityadmin;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  


