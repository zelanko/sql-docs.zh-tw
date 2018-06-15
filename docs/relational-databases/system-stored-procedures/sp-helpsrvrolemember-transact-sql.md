---
title: sp_helpsrvrolemember (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d4c800464cf0da918e748ba6b6c9d1ffc4c093a0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33250725"
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
 [  **@srvrolename =** ] **'***角色***'**  
 這是固定伺服器角色的名稱。 *角色*是**sysname**，預設值是 NULL。 如果*角色*未指定，結果集會包含所有固定的伺服器角色的相關資訊。  
  
 *角色*可以是下列值之一。  
  
|固定伺服器角色|Description|  
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
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|伺服器角色的名稱|  
|MemberName|**sysname**|伺服器角色的成員名稱|  
|MemberSID|**varbinary(85)**|成員名稱的安全性識別碼|  
  
## <a name="remarks"></a>備註  
 您可以使用 sp_helprolemember 來顯示資料庫角色的成員。  
  
 所有登入是公開的成員。 sp_helpsrvrolemember 無法辨識 public 角色，因為在內部，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會實作公開為角色。  
  
 若要加入或移除的成員的伺服器角色，請參閱[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
 sp_helpsrvrolemember 不會將使用者定義伺服器角色做為引數。 若要判斷使用者定義伺服器角色的成員，請參閱中的範例[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會列出 `sysadmin` 固定伺服器角色的成員。  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_helprole &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
