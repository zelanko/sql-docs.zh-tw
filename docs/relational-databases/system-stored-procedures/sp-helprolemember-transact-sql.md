---
title: sp_helprolemember & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 547ac1bce010e1f25eb2fce178844ff2b3f77bd1
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526940"
---
# <a name="sphelprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回目前資料庫中直屬角色成員的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] ' role '` 是目前資料庫中名稱。 *角色*已**sysname**，預設值是 NULL。 *角色*必須存在於目前的資料庫。 如果*角色*未指定，則會傳回包含從目前資料庫的至少一個成員的所有角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|目前資料庫中角色的名稱。|  
|**MemberName**|**sysname**|成員名稱**DbRole。**|  
|**MemberSID**|**varbinary(85)**|安全性識別元**成員名稱。**|  
  
## <a name="remarks"></a>備註  
 如果資料庫包含巢狀的角色**MemberName**可能是角色的名稱。 **sp_helprolemember**不會顯示經由巢狀角色取得的成員資格。 例如，如果 User1 是 Role1 的成員，而且 Role1 是 Role2 的成員，`EXEC sp_helprolemember 'Role2'`; 將會傳回 Role1，而不是 Role1 的成員 (此範例中為 User1)。 若要傳回巢狀成員資格，您必須執行**sp_helprolemember**針對每個巢狀角色重複。  
  
 使用**sp_helpsrvrolemember**来顯示固定的伺服器角色的成員。  
  
 使用[IS_ROLEMEMBER &#40;TRANSACT-SQL&#41; ](../../t-sql/functions/is-rolemember-transact-sql.md)來檢查指定的使用者角色成員資格。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 `Sales` 角色的成員。  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
