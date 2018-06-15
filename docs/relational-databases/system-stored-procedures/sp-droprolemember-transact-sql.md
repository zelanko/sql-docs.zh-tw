---
title: sp_droprolemember (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9bb4bf48955c2b8c2f3039aa9e8e0f68e097f516
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258550"
---
# <a name="spdroprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  從目前資料庫中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色移除安全性帳戶。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 這是要移除成員的角色名稱。 *角色*是**sysname**，沒有預設值。 *角色*必須存在於目前的資料庫。  
  
 [  **@membername =** ] **'***security_account***'**  
 這是從角色移除的安全性帳戶名稱。 *security_account*是**sysname**，沒有預設值。 *security_account*可以是資料庫使用者、 另一個資料庫角色、 Windows 登入或 Windows 群組。 *security_account*必須存在於目前的資料庫。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_droprolemember 從 sysmembers 資料表刪除資料列，從資料庫角色移除成員。 從角色中移除成員後，該成員會喪失該角色成員資格所具有的任何權限。  
  
 若要從固定的伺服器角色移除使用者，使用 sp_dropsrvrolemember。 無法從 public 角色中，移除使用者，無法從角色移除 dbo。  
  
 若要查看的成員使用 sp_helpuser[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]角色，並使用 ALTER ROLE 將成員新增至角色。  
  
## <a name="permissions"></a>Permissions  
 需要角色的 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從角色 `JonB` 中移除使用者 `Sales`。  
  
```  
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會從角色 `JonB` 中移除使用者 `Sales`。  
  
```  
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpuser &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

