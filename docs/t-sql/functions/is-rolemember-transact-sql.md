---
title: "IS_ROLEMEMBER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fb52e3460ed6c39d619453e370df310d530dd6a6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="isrolemember-transact-sql"></a>IS_ROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  指示指定的資料庫主體是否為指定之資料庫角色的成員。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
## <a name="arguments"></a>引數  
 **'** *角色* **'**  
 要檢查之資料庫角色的名稱。 *角色*是**sysname**。  
  
 **'** *database_principal* **'**  
 要檢查之資料庫使用者、資料庫角色或應用程式角色的名稱。 *database_principal*是**sysname**，預設值是 NULL。 如果未指定值，結果將以目前的執行內容為依據。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
|傳回值|Description|  
|------------------|-----------------|  
|0|*database_principal*不是成員的*角色*。|  
|1|*database_principal*隸屬*角色*。|  
|NULL|*database_principal*或*角色*不正確，或您沒有檢視角色成員資格的權限。|  
  
## <a name="remarks"></a>備註  
 請利用 IS_ROLEMEMBER 函數來判斷目前使用者是否能執行需要資料庫角色權限的動作。  
  
 如果*database_principal*根據 Windows 登入，例如 Contoso\Mary5，IS_ROLEMEMBER 會傳回 NULL，除非*database_principal*被授與或拒絕的直接存取至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 如果選擇性*database_principal*參數是未提供，而如果*database_principal*以 Windows 網域登入，它可能會透過 Windows 群組成員資格的資料庫角色的成員. 為了解析這類間接成員資格，IS_ROLEMEMBER 會要求網域控制站提供 Windows 群組成員資格資訊。 如果網域控制站無法存取或沒有回應，IS_ROLEMEMBER 只會藉由考量使用者及其本機群組，傳回角色成員資格資訊。 如果指定的使用者不是目前的使用者，IS_ROLEMEMBER 傳回的值可能會與驗證器 (如 Active Directory) 上一次對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料更新不同。  
  
 如果選擇性*database_principal*提供參數，則進行查詢的資料庫主體必須存在於 sys.database_principals，或 IS_ROLEMEMBER 將傳回 NULL。 這表示*database_principal*無效，無法在此資料庫中。  
  
 當*database_principal*參數為基礎的網域登入，或根據 Windows 群組和網域控制站無法存取，is_rolemember 的呼叫將會失敗，且可能傳回不正確或不完整的資料。  
  
 如果無法存取網域控制站，當 Windows 主體可以在本機上經過驗證時，IS_ROLEMEMBER 的呼叫將傳回正確的資訊，例如，本機 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 **IS_ROLEMEMBER** Windows 群組當做資料庫主體引數，而且這個 Windows 群組是另一個 Windows 群組成員的是，接著，指定的資料庫角色的成員時，一律傳回 0。  
  
 使用者帳戶控制 (UAC) 中找到[!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]和 Windows Server 2008 也可能會傳回不同的結果。 這會取決於使用者是以 Windows 群組成員還是特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的身分存取伺服器而定。  
  
 這個函數會評估角色成員資格，而非基礎權限。 例如， **db_owner**固定的資料庫角色擁有**CONTROL DATABASE**權限。 如果使用者具有**CONTROL DATABASE**權限但不是角色的成員，此函數將正確回報使用者不是成員的**db_owner**角色，即使使用者具有相同的權限。  
  
## <a name="related-functions"></a>相關函數  
 若要判斷目前使用者是否為指定的 Windows 群組的成員或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫角色中，使用[IS_MEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md). 若要判斷是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入伺服器角色的成員，請使用[IS_SRVROLEMEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 需要資料庫角色的 VIEW DEFINITION 權限。  
  
## <a name="examples"></a>範例  
 下列範例指出目前使用者是否為 `db_datareader` 固定資料庫角色的成員。  
  
```  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [更改角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [DROP ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [建立伺服器角色 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
