---
title: xp_logininfo (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5c214c8b061e2530c4dcf4b178b6028cbdca01fa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62644811"
---
# <a name="xplogininfo-transact-sql"></a>xp_logininfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關 Windows 使用者和 Windows 群組的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>引數  
`[ @acctname = ] 'account_name'` 是的 Windows 使用者或授與存取權的群組名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 *account_name*已**sysname**，預設值是 NULL。 如果*account_name*未指定，所有 Windows 群組和 Windows 使用者已被明確授都與登入權限會報告。 *account_name*必須是完整名稱。 例如，'ADVWKS4\macraes' 或 'BUILTIN\Administrators'。  
  
 **'all'** | **'members'**  
 指定是要報告有關帳戶所有權限路徑的資訊，或是要報告有關 Windows 群組成員的資訊。 **@option** 已**varchar(10)**，預設值是 NULL。 除非**所有**指定，會顯示的第一個權限路徑。  
  
`[ @privilege = ] variable_name` 會傳回指定的 Windows 帳戶的權限層級的輸出參數。 *variable_name*已**varchar(10)**，預設值是 'Not wanted'。 傳回的權限等級**使用者**， **admin**，或**null**。  
  
 OUTPUT  
 指定時，會將放*variable_name*輸出參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**account name**|**sysname**|完整的 Windows 帳戶名稱。|  
|**type**|**char(8)**|Windows 帳戶的類型。 有效值**使用者**或是**群組**。|  
|**privilege**|**char(9)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權限。 有效值**系統管理員**，**使用者**，或**null**。|  
|**對應的登入名稱**|**sysname**|使用者帳戶，具有使用者權限，如**對應登入名稱**會顯示對應的登入名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時它前面加上這個對應的規則使用的網域名稱的帳戶登入嘗試使用。|  
|**權限路徑**|**sysname**|允許帳戶存取權的群組成員資格。|  
  
## <a name="remarks"></a>備註  
 如果*account_name*指定，則**xp_logininfo**報告指定的 Windows 使用者或群組的最高的權限層級。 如果 Windows 使用者具有系統管理員和網域使用者的存取權，系統將回報這位使用者是系統管理員。 如果使用者是權限層級相等的多個 Windows 群組的成員，則只會回報第一個被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取權的群組。  
  
 如果*account_name*是有效的 Windows 使用者或群組不是與相關聯[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入，會傳回空的結果集。 如果*account_name*無法識別為有效的 Windows 使用者或群組，傳回錯誤訊息。  
  
 如果*account_name*並**所有**所指定，會傳回 Windows 使用者或群組的所有權限路徑。 如果*account_name*成員的多個群組，全部都已被授權存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，會傳回多個資料列。 **系統管理員**權限的資料列之前傳回**使用者**權限資料列，並在權限層級來傳回資料列的順序對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入所建立。  
  
 如果*account_name*並**成員**所指定，則傳回的下一個層級群組的成員的清單。 如果*account_name*是本機群組，則清單會包含本機使用者、 網域使用者和群組。 如果*account_name*是網域帳戶，清單由網域使用者所組成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須連接到網域控制器，才能擷取群組成員資格資訊。 如果伺服器無法連上網域控制器，就不會傳回任何資訊。  
  
 **xp_logininfo**只會傳回來自 Active Director 全域群組，非萬用群組的資訊。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定伺服器角色或成員資格**公用**固定的資料庫角色中**主要**具有 EXECUTE 權限授與的資料庫。  
  
## <a name="examples"></a>範例  
 下列範例會顯示相關的資訊`BUILTIN\Administrators`Windows 群組。  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
