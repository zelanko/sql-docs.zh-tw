---
title: "IS_SRVROLEMEMBER (TRANSACT-SQL) |Microsoft 文件"
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
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
caps.latest.revision: 65
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c26c0c1f4cb6a22f50cdc6a87d7a31f25b65e138
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="issrvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入是不是指定之伺服器角色的成員。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>引數  
 **'** *角色* **'**  
 這是要檢查的伺服器角色名稱。 *角色*是**sysname**。  
  
 有效值*角色*是使用者定義伺服器角色和下列固定伺服器角色：  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> public|  
|processadmin||  
  
 **'** *登入* **'**  
 名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]檢查登入。 *登入*是**sysname**，預設值是 NULL。 如果未指定值，結果將以目前的執行內容為依據。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
|傳回值|Description|  
|------------------|-----------------|  
|0|*登入*不是成員的*角色*。<br /><br /> 在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，這個陳述式一律傳回 0。|  
|1|*登入*隸屬*角色*。|  
|NULL|*角色*或*登入*不正確，或您沒有檢視角色成員資格的權限。|  
  
## <a name="remarks"></a>備註  
 若要判斷目前使用者是否能執行需要伺服器角色的權限的動作 UseIS_SRVROLEMEMBER。  
  
 如果指定的 Windows 登入，例如 Contoso\Mary5，*登入*， **IS_SRVROLEMEMBER**傳回**NULL**，除非您授與或拒絕的直接存取以之登入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 如果選擇性*登入*參數是未提供，而如果*登入*是 Windows 網域登入，它可能是透過 Windows 群組成員資格固定的伺服器角色的成員。 為了解析這類間接成員資格，IS_SRVROLEMEMBER 會要求網域控制站提供 Windows 群組成員資格資訊。 如果網域控制站無法存取或沒有回應， **IS_SRVROLEMEMBER**藉由考量使用者及其本機群組只會傳回角色成員資格資訊。 如果指定的使用者不是目前的使用者，IS_SRVROLEMEMBER 傳回的值可能會與驗證器 (如 Active Directory) 上一次對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料更新不同。  
  
 如果提供選用的登入參數，則進行查詢的 Windows 登入必須存在於 sys.server_principals 中，否則 IS_SRVROLEMEMBER 將傳回 NULL。 這表示登入無效。  
  
 當登入參數為網域登入或以 Windows 群組為基礎，而且無法存取網域控制站，IS_SRVROLEMEMBER 的呼叫將會失敗，而且可能會傳回不正確或不完整的資料。  
  
 如果無法存取網域控制站，當 Windows 主體可以在本機上經過驗證時，IS_SRVROLEMEMBER 的呼叫將傳回正確的資訊，例如，本機 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 **IS_SRVROLEMEMBER** Windows 群組做為登入引數和這個 Windows 群組是另一個 Windows 群組成員的是，接著，指定的伺服器角色的成員時，一律傳回 0。  
  
 使用者帳戶控制 (UAC) 設定也可能會導致傳回不同的結果。 這會取決於使用者是以 Windows 群組成員還是特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者的身分存取伺服器而定。  
  
 這個函數會評估角色成員資格，而非基礎權限。 例如， **sysadmin**固定的伺服器角色擁有**CONTROL SERVER**權限。 如果使用者具有**CONTROL SERVER**權限但不是角色的成員，此函數將正確回報使用者不是成員的**sysadmin**角色，即使使用者具有相同的權限。  
  
## <a name="related-functions"></a>相關函數  
 若要判斷目前使用者是否為指定的 Windows 群組的成員或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫角色中，使用[IS_MEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md). 若要判斷是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入是資料庫角色的成員，請使用[IS_ROLEMEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-rolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
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
  
 下列範例指出網域登入 Pat 是否為成員**diskadmin**固定的伺服器角色。  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>另請參閱  
 [IS_MEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

