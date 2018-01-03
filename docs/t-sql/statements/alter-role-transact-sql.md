---
title: "更改角色 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs: TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
caps.latest.revision: "64"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 897e8017965e71f345a93550e9af0c138d80b3b7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  加入或移除成員，或從資料庫角色，或變更使用者定義資料庫角色的名稱。  
  
> [!NOTE]  
>  若要改變角色中的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sp_addrolemember &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)和[sp_droprolemember &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```  
-- Syntax for SQL Server 2008 only  
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *role_name*  
 **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （從 2008年開始），  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要變更的資料庫角色。  
  
 加入成員*database_principal*l  
 **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （2012年起），  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要新增的資料庫主體的資料庫角色成員資格。  
  
-   *database_principal*是資料庫使用者定義資料庫角色。  
  
-   *database_principal*不能是固定的資料庫角色或伺服器主體。  
  
DROP MEMBER *database_principal*  
 **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （2012年起），  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要移除資料庫角色的成員資格的資料庫主體。  
  
-   *database_principal*是資料庫使用者定義資料庫角色。  
  
-   *database_principal*不能是固定的資料庫角色或伺服器主體。  
  
其中 NAME = *new_name*  
 **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （從 2008年開始），  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要變更使用者定義資料庫角色的名稱。 新的名稱必須在資料庫中已經存在。  
  
 變更資料庫角色的名稱不會變更識別碼、擁有者或角色的權限。  
  
## <a name="permissions"></a>Permissions  
 若要執行此命令，您需要一或多個這些權限或成員資格：  
  
-   **ALTER**角色的權限  
-   **ALTER ANY ROLE**資料庫的權限  
-   中的成員資格**db_securityadmin**固定的資料庫角色  
  
此外，若要變更固定的資料庫角色中的成員資格您需要：  
  
-   中的成員資格**db_owner**固定的資料庫角色  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 您無法變更固定的資料庫角色的名稱。  
  
## <a name="metadata"></a>中繼資料  
 這些系統檢視表包含資料庫角色和資料庫主體的相關資訊。  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>範例  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. 變更資料庫角色的名稱  
 **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （從 2008年開始），  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 下列範例會將角色 `buyers` 的名稱改成 `purchasing`。 [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```sql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. 新增或移除角色的成員  
 **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （2012年起），  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 這個範例會建立名為的資料庫角色`Sales`。 它加入至成員資格，名為 Barry 資料庫使用者，並顯示如何移除成員 Barry。 [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```sql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>請參閱  
 [建立角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
