---
title: xp_logininfo （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logininfo_TSQL
- xp_logininfo
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logininfo
ms.assetid: ee7162b5-e11f-4a0e-a09c-1878814dbbbd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b5a1a7067e1ebda150d0236020288514eb90a8fc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890733"
---
# <a name="xp_logininfo-transact-sql"></a>xp_logininfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回有關 Windows 使用者和 Windows 群組的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>引數  
`[ @acctname = ] 'account_name'`這是已授與存取權之 Windows 使用者或群組的名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *account_name*是**sysname**，預設值是 Null。 如果未指定*account_name* ，就會報告已明確授與登入許可權的所有 windows 群組和 windows 使用者。 *account_name*必須是完整的。 例如，'ADVWKS4\macraes' 或 'BUILTIN\Administrators'。  
  
 **' all '**  | [**成員**]  
 指定是要報告有關帳戶所有權限路徑的資訊，或是要報告有關 Windows 群組成員的資訊。 ** \@ option**是**Varchar （10）**，預設值是 Null。 除非指定**all** ，否則只會顯示第一個許可權路徑。  
  
`[ @privilege = ] variable_name`這是傳回指定 Windows 帳戶之許可權層級的輸出參數。 *variable_name*為**Varchar （10）**，預設值為「不需要」。 傳回的許可權層級為 [**使用者**]、[系統**管理員**] 或 [ **null**]。  
  
 OUTPUT  
 當指定時，會將*variable_name*放在輸出參數中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**帳戶名稱**|**sysname**|完整的 Windows 帳戶名稱。|  
|**type**|**char （8）**|Windows 帳戶的類型。 有效值為 [**使用者**] 或 [**群組**]。|  
|**特權**|**char(9)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權限。 有效的值為**admin**、 **user**或**null**。|  
|**mapped login name**|**sysname**|對於具有「使用者」許可權的使用者帳戶，**對應的登入名稱**會顯示在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 此帳戶登入時嘗試使用的對應登入名稱，其方式是在其前面加入的功能變數名稱。|  
|**permission path**|**sysname**|允許帳戶存取權的群組成員資格。|  
  
## <a name="remarks"></a>備註  
 如果指定了*account_name* ， **xp_logininfo**會報告指定之 Windows 使用者或群組的最高許可權層級。 如果 Windows 使用者具有系統管理員和網域使用者的存取權，系統將回報這位使用者是系統管理員。 如果使用者是權限層級相等的多個 Windows 群組的成員，則只會回報第一個被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取權的群組。  
  
 如果*account_name*是不是與登入相關聯的有效 Windows 使用者或群組 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則會傳回空的結果集。 如果*account_name*無法識別為有效的 Windows 使用者或群組，則會傳回錯誤訊息。  
  
 如果*account_name*並指定**all** ，則會傳回 Windows 使用者或群組的擁有權限路徑。 如果*account_name*是多個群組的成員，則所有已被授與存取權 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，就會傳回多個資料列。 系統**管理員**許可權資料列會在**使用者**權力資料列之前傳回，而許可權層級資料列內則會依照對應登入建立的順序傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 如果指定*account_name*和**成員**，則會傳回群組的下一個層級成員清單。 如果*account_name*是本機群組，清單可以包含 [本機使用者]、[網域使用者] 和 [群組]。 如果*account_name*是網域帳戶，則此清單是由網域使用者所組成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須連接到網域控制器，才能擷取群組成員資格資訊。 如果伺服器無法連上網域控制器，就不會傳回任何資訊。  
  
 **xp_logininfo**只會傳回來自 Active Directory 全域群組（而非萬用群組）的資訊。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定伺服器角色中的成員資格，或**master**資料庫中已授與 EXECUTE 許可權之**公用**固定資料庫角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 Windows 群組的相關資訊 `BUILTIN\Administrators` 。  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_denylogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql 的一般擴充預存程式&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
