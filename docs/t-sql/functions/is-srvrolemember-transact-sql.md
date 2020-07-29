---
title: IS_SRVROLEMEMBER (Transact-SQL)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: eb44adf219905a585b922fc280215f1c81465cda
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248507"
---
# <a name="is_srvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是不是指定之伺服器角色的成員。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 **'** *role* **'**  
 這是要檢查的伺服器角色名稱。 *role* 為 **sysname**。  
  
 *role* 的有效值是使用者定義的伺服器角色和下列固定伺服器角色：  

- 系統管理員 (sysadmin)
- serveradmin
- dbcreator
- setupadmin  
- bulkadmin
- securityadmin  
- diskadmin
- 公開  
- processadmin
  
 **'** *login* **'**  
 為要檢查的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。 *login* 是預設值為 NULL 的 **sysname**。 如果未指定值，結果將以目前的執行內容為依據。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回型別  
 **int**  
  
|傳回值|描述|  
|------------------|-----------------|  
|0|*login* 不是 *role* 的成員。<br /><br /> 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，這個陳述式一律會傳回 0。|  
|1|*login* 為 *role* 的成員。|  
|NULL|*role* 或 *login* 無效，或是您沒有檢視角色成員資格的權限。|  
  
## <a name="remarks"></a>備註  
 請使用 IS_SRVROLEMEMBER 函式來判斷目前使用者是否能執行需要伺服器角色權限的動作。  
  
 如果針對 *login* 指定 Windows 登入 (例如 Contoso\Mary5)，**IS_SRVROLEMEMBER** 就會傳回 **NULL**，除非此登入已被授與或拒絕 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的直接存取權。  
  
 如果未提供選用的 *login* 參數，而且如果 *login* 是 Windows 網域登入，則其可能是藉由 Windows 群組中的成員資格而成為固定伺服器角色的成員。 為了解析這類間接成員資格，IS_SRVROLEMEMBER 會要求網域控制站提供 Windows 群組成員資格資訊。 如果網域控制站無法存取或沒有回應，**IS_SRVROLEMEMBER** 只會藉由考量使用者及其本機群組，傳回角色成員資格資訊。 如果指定的使用者不是目前的使用者，IS_SRVROLEMEMBER 傳回的值可能會與驗證器 (如 Active Directory) 上一次對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料更新不同。  
  
 如果提供選用的登入參數，則進行查詢的 Windows 登入必須存在於 sys.server_principals 中，否則 IS_SRVROLEMEMBER 將傳回 NULL。 這表示登入無效。  
  
 當登入參數為網域登入或以 Windows 群組為基礎，而且無法存取網域控制站，IS_SRVROLEMEMBER 的呼叫將會失敗，而且可能會傳回不正確或不完整的資料。  
  
 如果無法存取網域控制站，當 Windows 主體可以在本機上經過驗證時，IS_SRVROLEMEMBER 的呼叫將傳回正確的資訊，例如，本機 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 當 Windows 群組當作登入引數來使用，而且這個 Windows 群組是另一個 Windows 群組的成員，而後者群組又是指定之伺服器角色的成員時，**IS_SRVROLEMEMBER** 一律傳回 0。  
  
 使用者帳戶控制 (UAC) 設定也可能會導致傳回不同的結果。 這會取決於使用者是以 Windows 群組成員還是特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的身分存取伺服器而定。  
  
 這個函數會評估角色成員資格，而非基礎權限。 例如，**sysadmin** 固定伺服器角色擁有 **CONTROL SERVER** 權限。 如果使用者擁有 **CONTROL SERVER** 權限，但不是此角色的成員，這個函式將正確回報該使用者不是 **sysadmin** 角色的成員，即使該使用者擁有相同的權限也一樣。  
  
## <a name="related-functions"></a>相關函數  
 若要判斷目前使用者是否為指定之 Windows 群組或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色的成員，請使用 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)。 若要判斷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是否為資料庫角色的成員，請使用 [IS_ROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-rolemember-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 需要伺服器角色的 VIEW DEFINITION 權限。  
  
## <a name="examples"></a>範例  
 下列範例指出目前使用者的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是否為系統管理員 (`sysadmin`) 固定伺服器角色的成員。  
  
```  
IF IS_SRVROLEMEMBER ('sysadmin') = 1  
   print 'Current user''s login is a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') = 0  
   print 'Current user''s login is NOT a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') IS NULL  
   print 'ERROR: The server role specified is not valid.';  
```  
  
 下列範例指出網域登入 Pat 是否為 **diskadmin** 固定伺服器角色的成員。  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>另請參閱  
 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
