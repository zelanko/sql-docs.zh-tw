---
title: IS_MEMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IS_MEMBER
- IS_MEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], members
- current member status
- roles [SQL Server], members
- testing member status
- members [SQL Server]
- checking member status
- IS_MEMBER function
- verifying member status
- groups [SQL Server], members
- members [SQL Server], verifying
ms.assetid: 77cb68a0-19b7-4fe1-ab17-e5587699631b
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1344b307aca66f5850cfc2806899814f53495e61
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87110994"
---
# <a name="is_member-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  指出目前使用者是指定之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 群組或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色的成員。 Azure Active Directory 群組不支援 IS_MEMBER 函式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 **'** *group* **'**  
**適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本
  
 這是所檢查之 Windows 群組的名稱；格式必須為 *Domain*\\*Group*。 *group* 為 **sysname**。  
  
 **'** *role* **'**  
 這是要檢查的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色名稱。 *role* 為 **sysname**，而且可以包含資料庫固定角色或使用者定義角色，但無法包含伺服器角色。  
  
## <a name="return-types"></a>傳回型別  
 **int**  
  
## <a name="remarks"></a>備註  
 IS_MEMBER 會傳回下列值。  
  
|傳回值|描述|  
|------------------|-----------------|  
|0|目前使用者不是 *group* 或 *role* 的成員。|  
|1|目前使用者是 *group* 或 *role* 的成員。|  
|NULL|任一 *group* 或 *role* 無效。 透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或使用應用程式角色的登入進行查詢時，針對 Windows 群組傳回 NULL。|  
  
 IS_MEMBER 會檢查 Windows 所建立的存取 Token 來判斷 Windows 群組成員資格。 存取 Token 不會反映在使用者連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之後，所進行的群組成員資格變更。 Windows 群組成員資格無法透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應用程式角色進行查詢。  
  
 若要從資料庫角色中新增和移除成員，請使用 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)。 若要從伺服器角色中新增和移除成員，請使用 [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
 這個函數會評估角色成員資格，而非基礎權限。 例如，**db_owner** 固定資料庫角色具有 **CONTROL DATABASE** 權限。 如果使用者擁有 **CONTROL DATABASE** 權限，但不是此角色的成員，則這個函式將正確回報該使用者不是 **db_owner** 角色的成員，即使該使用者擁有相同的權限也一樣。  
  
 **sysadmin** 固定伺服器角色的成員會作為 **dbo** 使用者輸入每個資料庫。 若要檢查 **sysadmin** 固定伺服器角色成員的權限，請檢查 **dbo** 的權限，而非原始登入。 由於 **dbo** 無法新增至資料庫角色，也不存在於 Windows 群組之中，因此 **dbo** 一律會傳回 0 (或當角色不存在時，傳回 NULL)。  
  
## <a name="related-functions"></a>相關函數  
 若要判斷另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是否為資料庫角色的成員，請使用 [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md)。 若要判斷另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是否為伺服器角色的成員，請使用 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)。  
  
## <a name="examples"></a>範例  
 下列範例會檢查目前使用者是資料庫角色或 Windows 網域群組的成員。  
  
```  
-- Test membership in db_owner and print appropriate message.  
IF IS_MEMBER ('db_owner') = 1  
   PRINT 'Current user is a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') = 0  
   PRINT 'Current user is NOT a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') IS NULL  
   PRINT 'ERROR: Invalid group / role specified';  
GO  
  
-- Execute SELECT if user is a member of ADVWORKS\Shipping.  
IF IS_MEMBER ('ADVWORKS\Shipping') = 1  
   SELECT 'User ' + USER + ' is a member of ADVWORKS\Shipping.';   
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
