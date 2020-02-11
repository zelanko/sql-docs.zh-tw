---
title: sp_droprolemember （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprolemember_TSQL
- sp_droprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprolemember
ms.assetid: c2f19ab1-e742-4d56-ba8e-8ffd40cf4925
ms.author: vanto
author: VanMSFT
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7123c1bd3fee61a3d0671a0d8fbe27c2943ba7ea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68124853"
---
# <a name="sp_droprolemember-transact-sql"></a>sp_droprolemember (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  從目前資料庫中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色移除安全性帳戶。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  

### <a name="syntax-for-both-sql-server-and-azure-sql-database"></a>SQL Server 和 Azure SQL Database 的語法

```  
sp_droprolemember [ @rolename = ] 'role' ,   
     [ @membername = ] 'security_account'  
```  

### <a name="syntax-for-both-azure-sql-data-warehouse-and-parallel-data-warehouse"></a>Azure SQL 資料倉儲和平行處理資料倉儲的語法

```  
sp_droprolemember 'role' ,  
     'security_account'  
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] 'role'`這是要從中移除成員的角色名稱。 *role*是**sysname**，沒有預設值。 *角色*必須存在於目前的資料庫中。  
  
`[ @membername = ] 'security_account'`這是從角色移除的安全性帳戶名稱。 *security_account*是**sysname**，沒有預設值。 *security_account*可以是資料庫使用者、另一個資料庫角色、windows 登入或 windows 群組。 *security_account*必須存在於目前的資料庫中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 sp_droprolemember 藉由刪除 sysmembers 資料表中的資料列，將成員從資料庫角色中移除。 從角色中移除成員後，該成員會喪失該角色成員資格所具有的任何權限。  
  
 若要從固定伺服器角色中移除使用者，請使用 sp_dropsrvrolemember。 您無法從 public 角色中移除使用者，也不能從任何角色中移除 dbo。  
  
 使用 sp_helpuser 查看[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]角色的成員，並使用 ALTER role 將成員新增至角色。  
  
## <a name="permissions"></a>權限  
 需要角色的 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從角色 `JonB` 中移除使用者 `Sales`。  
  
```sql
EXEC sp_droprolemember 'Sales', 'Jonb';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會從角色 `JonB` 中移除使用者 `Sales`。  
  
```sql
EXEC sp_droprolemember 'Sales', 'JonB'  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

