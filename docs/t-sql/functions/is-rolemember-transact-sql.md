---
description: IS_ROLEMEMBER (Transact-SQL)
title: IS_ROLEMEMBER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IS_ROLEMEMBER
- IS_ROLEMEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_ROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 73efa688-ae91-4014-98bc-1cabe47321f7
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 856265d1ba66eb2cfae29b12ec23b432cb4c8e3f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "91116717"
---
# <a name="is_rolemember-transact-sql"></a>IS_ROLEMEMBER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  指示指定的資料庫主體是否為指定之資料庫角色的成員。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 **'** *role* **'**  
 要檢查之資料庫角色的名稱。 *role* 為 **sysname**。  
  
 **'** *database_principal* **'**  
 要檢查之資料庫使用者、資料庫角色或應用程式角色的名稱。 *database_principal* 為具有 NULL 預設值的 **sysname**。 如果未指定值，結果將以目前的執行內容為依據。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回型別  
 **int**  
  
|傳回值|描述|  
|------------------|-----------------|  
|0|*database_principal* 不是 *role* 的成員。|  
|1|*database_principal* 是 *role* 的成員。|  
|NULL|*database_principal* 或 *role* 無效，或是您沒有檢視角色成員資格的權限。|  
  
## <a name="remarks"></a>備註  
 請利用 IS_ROLEMEMBER 函數來判斷目前使用者是否能執行需要資料庫角色權限的動作。  
  
 若 *database_principal* 是以 Windows 登入為基礎 (例如 Contoso\Mary5)，除非 *database_principal* 已獲得授與或拒絕直接存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的權限，否則 IS_ROLEMEMBER 會傳回 NULL。  
  
 如果未提供選擇性的 *database_principal* 參數，而且如果 *database_principal* 是以 Windows 網域登入為基礎，它可能是藉由 Windows 群組中的成員資格而成為資料庫角色的成員。 為了解析這類間接成員資格，IS_ROLEMEMBER 會要求網域控制站提供 Windows 群組成員資格資訊。 如果網域控制站無法存取或沒有回應，IS_ROLEMEMBER 只會藉由考量使用者及其本機群組，傳回角色成員資格資訊。 如果指定的使用者不是目前的使用者，IS_ROLEMEMBER 傳回的值可能會與驗證器 (如 Active Directory) 上一次對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料更新不同。  
  
 如果已提供選擇性 *database_principal* 參數，則進行查詢的資料庫主體必須存在於 sys.database_principals 中，否則 IS_ROLEMEMBER 將傳回 NULL。 這表示 *database_principal* 在此資料庫中無效。  
  
 當 *database_principal* 以網域登入或以 Windows 群組為基礎，而且無法存取網域控制站，IS_ROLEMEMBER 的呼叫將會失敗，而且可能會傳回不正確或不完整的資料。  
  
 如果無法存取網域控制站，當 Windows 主體可以在本機上經過驗證時，IS_ROLEMEMBER 的呼叫將傳回正確的資訊，例如，本機 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 當 Windows 群組當作資料庫主體引數來使用，而且這個 Windows 群組是另一個 Windows 群組的成員，而其又是指定之資料庫角色的成員時，**IS_ROLEMEMBER** 一律會傳回 0。  
  
 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] 和 Windows Server 2008 中找到的使用者帳戶控制 (UAC) 也可能會傳回不同的結果。 這會取決於使用者是以 Windows 群組成員還是特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的身分存取伺服器而定。  
  
 這個函數會評估角色成員資格，而非基礎權限。 例如，**db_owner** 固定資料庫角色具有 **CONTROL DATABASE** 權限。 如果使用者擁有 **CONTROL DATABASE** 權限，但不是此角色的成員，則這個函式將正確回報該使用者不是 **db_owner** 角色的成員，即使該使用者擁有相同的權限也一樣。  
  
## <a name="related-functions"></a>相關函數  
 若要判斷目前使用者是否為指定之 Windows 群組或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色的成員，請使用 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)。 若要判斷另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是否為伺服器角色的成員，請使用 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 需要資料庫角色的 VIEW DEFINITION 權限。  
  
## <a name="examples"></a>範例  
 下列範例指出目前使用者是否為 `db_datareader` 固定資料庫角色的成員。  
  
```sql  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
