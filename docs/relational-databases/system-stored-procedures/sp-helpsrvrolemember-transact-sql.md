---
title: sp_helpsrvrolemember (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 618ec7d83ab8abce8cf201cb0b59033b808178c0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533490"
---
# <a name="sphelpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定伺服器角色成員的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @srvrolename = ] 'role'` 是固定的伺服器角色的名稱。 *角色*已**sysname**，預設值是 NULL。 如果*角色*未指定，結果集會包含所有固定的伺服器角色的相關資訊。  
  
 *角色*可以是下列值之一。  
  
|固定伺服器角色|描述|  
|-----------------------|-----------------|  
|sysadmin|系統管理員|  
|securityadmin|安全性管理員|  
|serveradmin|伺服器管理員|  
|setupadmin|安裝管理員|  
|processadmin|處理序管理員|  
|diskadmin|磁碟管理員|  
|dbcreator|資料庫建立者|  
|bulkadmin|可以執行 BULK INSERT 陳述式|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|伺服器角色的名稱|  
|MemberName|**sysname**|伺服器角色的成員名稱|  
|MemberSID|**varbinary(85)**|成員名稱的安全性識別碼|  
  
## <a name="remarks"></a>備註  
 您可以使用 sp_helprolemember 來顯示資料庫角色的成員。  
  
 所有登入是公開的成員。 sp_helpsrvrolemember 無法辨識的 public 角色，因為在內部，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會實作公開做為角色。  
  
 若要新增或移除的成員，從伺服器角色，請參閱[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
 sp_helpsrvrolemember 不會做為引數的使用者定義伺服器角色。 若要判斷使用者定義伺服器角色的成員，請參閱中的範例[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會列出 `sysadmin` 固定伺服器角色的成員。  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
