---
title: xp_logininfo (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_logininfo_TSQL
- xp_logininfo
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logininfo
ms.assetid: ee7162b5-e11f-4a0e-a09c-1878814dbbbd
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3eb400fed1fe0cbd25ef884dc56a89fe448717fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
 [  **@acctname =** ] **'***account_name***'**  
 這是獲得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取權之 Windows 使用者或群組的名稱。 *account_name*是**sysname**，預設值是 NULL。 如果*account_name*未指定，所有的 Windows 群組和 Windows 使用者之已被明確授與登入權限會報告。 *account_name*必須是完整名稱。 例如，'ADVWKS4\macraes' 或 'BUILTIN\Administrators'。  
  
 **'all'** | **'members'**  
 指定是要報告有關帳戶所有權限路徑的資訊，或是要報告有關 Windows 群組成員的資訊。 **@option** 是**varchar （10)**，預設值是 NULL。 除非**所有**指定，會顯示的第一個權限路徑。  
  
 [  **@privilege =** ] *variable_name*  
 這是傳回指定 Windows 帳戶權限層級的輸出參數。 *variable_name*是**varchar （10)**，預設值是 'Not wanted'。 權限層級傳回為**使用者**， **admin**，或**null**。  
  
 OUTPUT  
 當指定，會將置於*variable_name*輸出參數。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**帳戶名稱**|**sysname**|完整的 Windows 帳戶名稱。|  
|**type**|**char （8)**|Windows 帳戶的類型。 有效值為**使用者**或**群組**。|  
|**權限**|**char(9)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的存取權限。 有效值為**admin**，**使用者**，或**null**。|  
|**對應的登入名稱**|**sysname**|針對具有使用者權限，使用者帳戶**對應登入名稱**顯示對應的登入名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]便會嘗試使用時所使用的網域名稱的對應的規則，此帳戶登入加在它前面。|  
|**權限路徑**|**sysname**|允許帳戶存取權的群組成員資格。|  
  
## <a name="remarks"></a>備註  
 如果*account_name*指定，則**xp_logininfo**報告指定之 Windows 使用者或群組的最高的權限層級。 如果 Windows 使用者具有系統管理員和網域使用者的存取權，系統將回報這位使用者是系統管理員。 如果使用者是權限層級相等的多個 Windows 群組的成員，則只會回報第一個被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取權的群組。  
  
 如果*account_name*是有效的 Windows 使用者或群組不是與相關聯[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入，會傳回空的結果集。 如果*account_name*無法識別為有效的 Windows 使用者或群組，傳回錯誤訊息。  
  
 如果*account_name*和**所有**所指定，會傳回 Windows 使用者或群組的所有權限路徑。 如果*account_name*是已授與所有的存取權的多個群組，成員[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，會傳回多個資料列。 **Admin**權限資料列之前傳回則**使用者**權限資料列，並在權限層級來傳回資料列的順序對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前建立登入。  
  
 如果*account_name*和**成員**所指定，會傳回下一個層級成員的群組清單。 如果*account_name*是本機群組，則清單會包含本機使用者、 網域使用者和群組。 如果*account_name*是網域帳戶，清單由網域使用者所組成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須連接到網域控制器，才能擷取群組成員資格資訊。 如果伺服器無法連上網域控制器，就不會傳回任何資訊。  
  
 **xp_logininfo**資訊只會傳回來自 Active Director 全域群組，非萬用群組。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定伺服器角色或中的成員資格**公用**固定的資料庫角色中**主要**具有 EXECUTE 權限授與資料庫。  
  
## <a name="examples"></a>範例  
 下列範例會顯示有關的資訊`BUILTIN\Administrators`Windows 群組。  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
