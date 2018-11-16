---
title: ALTER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 51a50d8798dc05ee012d7da9848e45a759b7d9cb
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701396"
---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在資料庫角色中加入或移除成員，或變更使用者定義資料庫角色的名稱。  
  
> [!NOTE]  
>  若要改變 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 或 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 中的角色新增或成員卸除，請使用 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 和 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)。  
  
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
-- Syntax for SQL Server 2008, Azure SQL Data Warehouse and Parallel Data Warehouse
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *role_name*  
 **適用於：**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 2008 起)，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要變更的資料庫角色。  
  
 ADD MEMBER *database_principal*l  
 **適用於：**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 2012 起)，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要將資料庫主體新增至資料庫角色成員資格中。  
  
-   *database_principal* 可以是資料庫使用者或使用者定義的資料庫角色。  
  
-   *database_principal* 不能是固定資料庫角色或伺服器主體。  
  
DROP MEMBER *database_principal*  
 **適用於：**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 2012 起)，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要從資料庫角色成員資格移除資料庫主體。  
  
-   *database_principal* 可以是資料庫使用者或使用者定義的資料庫角色。  
  
-   *database_principal* 不能是固定資料庫角色或伺服器主體。  
  
WITH NAME = *new_name*  
 **適用於：**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 2008 起)，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 指定要變更使用者定義資料庫角色的名稱。 新的名稱不得已存在於資料庫中。  
  
 變更資料庫角色的名稱不會變更識別碼、擁有者或角色的權限。  
  
## <a name="permissions"></a>[權限]  
 若要執行此命令，您需要一或多個這些權限或成員資格：  
  
-   角色的 **ALTER** 權限  
-   資料庫的 **ALTER ANY ROLE** 權限  
-   **db_securityadmin** 固定資料庫角色中的成員資格  
  
此外，若要變更您所需要之固定資料庫角色中的成員資格：  
  
-   **db_owner** 固定資料庫角色中的成員資格  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 您無法變更固定資料庫角色的名稱。  
  
## <a name="metadata"></a>中繼資料  
 這些系統檢視包含資料庫角色和資料庫主體的相關資訊。  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>範例  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. 變更資料庫角色的名稱  
 **適用於：**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 2008 起)，[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 下列範例會將角色 `buyers` 的名稱改成 `purchasing`。   這個範例可以在 [AdventureWorks (英文)](https://msftdbprodsamples.codeplex.com/) 範例資料庫中執行。
  
```sql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. 新增或移除角色成員  
 **適用於：**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 2012 起)，[!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 這個範例會建立名為 `Sales` 的新資料庫。 它會將名稱為 Barry 的資料庫使用者加入至成員資格中，然後顯示如何移除成員 Barry。   這個範例可以在 [AdventureWorks (英文)](https://msftdbprodsamples.codeplex.com/) 範例資料庫中執行。
  
```sql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
