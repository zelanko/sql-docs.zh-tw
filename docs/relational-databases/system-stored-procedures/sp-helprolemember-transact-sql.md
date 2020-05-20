---
title: sp_helprolemember （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 65a1f4d2098e55c7007bd04e2fef00bcbac30ffc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824413"
---
# <a name="sp_helprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回目前資料庫中直屬角色成員的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] ' role '`這是目前資料庫中的角色名稱。 *role*是**sysname**，預設值是 Null。 *角色*必須存在於目前的資料庫中。 如果未指定*role* ，則會傳回至少包含一個來自目前資料庫之成員的所有角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|目前資料庫中角色的名稱。|  
|**MemberName**|**sysname**|DbRole 成員的名稱 **。**|  
|**MemberSID**|**Varbinary （85）**|**成員名稱**的安全識別碼。|  
  
## <a name="remarks"></a>備註  
 如果資料庫包含嵌套角色，**成員**名稱可以是角色的名稱。 **sp_helprolemember**不會顯示透過嵌套角色取得的成員資格。 例如，如果 User1 是 Role1 的成員，而且 Role1 是 Role2 的成員，`EXEC sp_helprolemember 'Role2'`; 將會傳回 Role1，而不是 Role1 的成員 (此範例中為 User1)。 若要傳回嵌套的成員資格，您必須針對每個嵌套角色重複執行**sp_helprolemember** 。  
  
 使用 [ **sp_helpsrvrolemember**顯示固定伺服器角色的成員。  
  
 使用[IS_ROLEMEMBER &#40;transact-sql&#41;](../../t-sql/functions/is-rolemember-transact-sql.md)來檢查指定使用者的角色成員資格。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 `Sales` 角色的成員。  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
