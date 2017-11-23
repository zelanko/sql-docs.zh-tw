---
title: "IS_MEMBER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_MEMBER
- IS_MEMBER_TSQL
dev_langs: TSQL
helpviewer_keywords:
- database roles [SQL Server], members
- current member status
- roles [SQL Server], members
- testing member status
- members [SQL Server]
- checking member status
- IS_MEMBER function
- verifying member status
- groups [SQL Server], members
- members [SQL Server], verifying
ms.assetid: 77cb68a0-19b7-4fe1-ab17-e5587699631b
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e14fc4cf70066c21a8a837760d4325a19ae4ff1c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="ismember-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指出目前使用者是指定之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 群組或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色的成員。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>引數  
 **'** *群組* **'**  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 正在檢查; 之 Windows 群組名稱必須是格式*網域*\\*群組*。 *群組*是**sysname**。  
  
 **'** *角色* **'**  
 名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所檢查的角色。 *角色*是**sysname**而且可以包含資料庫固定角色或使用者定義角色，但不是伺服器角色。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 IS_MEMBER 會傳回下列值。  
  
|傳回值|Description|  
|------------------|-----------------|  
|0|目前使用者不是屬於*群組*或*角色*。|  
|1|目前使用者所屬的*群組*或*角色*。|  
|NULL|任一*群組*或*角色*不正確。 透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或使用應用程式角色的登入進行查詢時，針對 Windows 群組傳回 NULL。|  
  
 IS_MEMBER 會檢查 Windows 所建立的存取 Token 來判斷 Windows 群組成員資格。 存取 Token 不會反映在使用者連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之後，所進行的群組成員資格變更。 無法查詢 Windows 群組成員資格[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]應用程式角色。  
  
 若要加入及移除資料庫角色的成員，使用[ALTER ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md). 新增和移除伺服器角色的成員，請使用[ALTER SERVER ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 這個函數會評估角色成員資格，而非基礎權限。 例如， **db_owner**固定的資料庫角色擁有**CONTROL DATABASE**權限。 如果使用者具有**CONTROL DATABASE**權限但不是角色的成員，此函數將正確回報使用者不是成員的**db_owner**角色，即使使用者具有相同的權限。  
  
 成員**sysadmin**固定的伺服器角色的輸入為每個資料庫**dbo**使用者。 檢查權限的成員**sysadmin**固定的伺服器角色，會檢查權限**dbo**，不是原始登入。 因為**dbo**不能加入至資料庫角色，而且不存在於 Windows 群組**dbo**一律會傳回 0 （或如果角色不存在則為 NULL）。  
  
## <a name="related-functions"></a>相關函數  
 若要判斷是否有另一個[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入是資料庫角色的成員，請使用[IS_ROLEMEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-rolemember-transact-sql.md). 若要判斷是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入伺服器角色的成員，請使用[IS_SRVROLEMEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="examples"></a>範例  
 下列範例會檢查目前使用者是資料庫角色或 Windows 網域群組的成員。  
  
```  
-- Test membership in db_owner and print appropriate message.  
IF IS_MEMBER ('db_owner') = 1  
   PRINT 'Current user is a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') = 0  
   PRINT 'Current user is NOT a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') IS NULL  
   PRINT 'ERROR: Invalid group / role specified';  
GO  
  
-- Execute SELECT if user is a member of ADVWORKS\Shipping.  
IF IS_MEMBER ('ADVWORKS\Shipping') = 1  
   SELECT 'User ' + USER + ' is a member of ADVWORKS\Shipping.';   
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [IS_SRVROLEMEMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
