---
title: sp_helpsrvrole (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrole_TSQL
- sp_helpsrvrole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrole
ms.assetid: 5c7f39f3-c261-4f70-8beb-08242d4ac242
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3addbb80d8423147a34c5b9fd9b1e3eab29471ab
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpsrvrole-transact-sql"></a>sp_helpsrvrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定伺服器角色的清單。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@srvrolename=** ] **'***角色***'**  
 這是固定伺服器角色的名稱。 *角色*是**sysname**，預設值是 NULL。 *角色*可以是下列值之一。  
  
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
|Description|**sysname**|伺服器角色的描述|  
  
## <a name="remarks"></a>備註  
 固定伺服器角色定義於伺服器層級，具有執行特定伺服器層級管理活動的權限。 固定伺服器角色無法加入、移除或變更。  
  
 若要加入或移除的成員的伺服器角色，請參閱[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
 所有登入是公開的成員。 sp_helpsrvrole 無法辨識 public 角色，因為在內部，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會實作公開為角色。  
  
 sp_helpsrvrole 不會將使用者定義伺服器角色做為引數。 若要列出的使用者定義伺服器角色，請參閱中的範例[ALTER SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-the-fixed-server-roles"></a>A. 列出固定伺服器角色  
 下列查詢會傳回固定伺服器角色的清單。  
  
```  
EXEC sp_helpsrvrole ;  
```  
  
### <a name="b-listing-fixed-and-user-defined-server-roles"></a>B. 列出固定和使用者定義的伺服器角色  
 下列查詢會傳回固定和使用者定義伺服器角色的清單。  
  
```  
SELECT * FROM sys.server_principals WHERE type = 'R' ;  
```  
  
### <a name="c-returning-a-description-of-a-fixed-server-role"></a>C. 傳回固定伺服器角色的描述  
 下列查詢會傳回 `diskadmin` 固定伺服器角色的名稱和描述。  
  
```  
sp_helpsrvrole 'diskadmin' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [伺服器層級角色](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
