---
title: sp_helprotect （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprotect
- sp_helprotect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprotect
ms.assetid: faaa3e40-1c95-43c2-9fdc-c61a1d3cc0c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7db43df5d500e56e58e3e8465ac03158fe7e4d21
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67997481"
---
# <a name="sp_helprotect-transact-sql"></a>sp_helprotect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回報表，報表中有目前資料庫中之物件的使用者權限或陳述式權限的相關資訊。  
  
> [!IMPORTANT]  
>  **sp_helprotect**不會傳回中[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]所引進之安全性實體的相關資訊。 請改用[sys.databases database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)和[fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md) 。  
  
 不會列出一律指派給固定伺服器角色或固定資料庫角色的權限。 不包括依本身在角色中的成員資格獲得權限的登入或使用者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helprotect [ [ @name = ] 'object_statement' ]   
     [ , [ @username = ] 'security_account' ]   
     [ , [ @grantorname = ] 'grantor' ]   
     [ , [ @permissionarea = ] 'type' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'object_statement'`這是目前資料庫中的物件名稱，或是具有要報告之許可權的語句。 *object_statement*是**Nvarchar （776）**，預設值是 Null，它會傳回所有物件和語句許可權。 如果值是物件 (資料表、檢視、預存程序或擴充預存程序)，它必須是目前資料庫中的有效物件。 物件名稱可以包含「_擁有_者」形式的擁有者辨識符號 **。**_物件_。  
  
 如果*object_statement*是語句，它可以是 CREATE 語句。  
  
`[ @username = ] 'security_account'`這是傳回許可權之主體的名稱。 *security_account*是**sysname**，預設值是 Null，它會傳回目前資料庫中的所有主體。 *security_account*必須存在於目前的資料庫中。  
  
`[ @grantorname = ] 'grantor'`這是授與許可權之主體的名稱。 授與者是**sysname**，預設*值是 Null* ，它會傳回資料庫中任何主體所授與之許可權的所有資訊。  
  
`[ @permissionarea = ] 'type'`這是一個字元字串，指出是否要顯示物件使用權限（字元字串**o**）、語句許可權（字元字串**s**），或兩者（**os**）。 *類型*為**Varchar （10）**，預設值為**os**。 *類型*可以是**o**和**s**的任何組合，在**o**和**s**之間不含逗號或空格。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**擁有者**|**sysname**|物件擁有者的名稱。|  
|**Object**|**sysname**|物件的名稱。|  
|**者**|**sysname**|對其授與權限之主體的名稱。|  
|**授與者**|**sysname**|對指定的被授與者授與權限之主體的名稱。|  
|**ProtectType**|**Nvarchar （10）**|保護類型的名稱：<br /><br /> GRANT REVOKE|  
|**動作**|**nvarchar(60)**|權限的名稱。 權限陳述式是否有效，需根據物件類型而定。|  
|**資料行**|**sysname**|權限的類型：<br /><br /> 全部 = 權限涵蓋物件的所有目前資料行。<br /><br /> 新增 = 權限涵蓋未來可能在物件上變更 (利用 ALTER 陳述式) 的任何新資料行。<br /><br /> 全部+新增 = 全部和新增的組合。<br /><br /> 如果權限類型不適用於資料行，則傳回句號。|  
  
## <a name="remarks"></a>備註  
 下列程序中的所有參數都是選擇性的。 如果執行時沒有設定任何參數，則 `sp_helprotect` 會顯示所有已在目前資料庫中授與或拒絕的權限。  
  
 如果只指定了部份 (而非全部) 參數，請利用具名參數來識別特定參數，或識別作為預留位置的 `NULL`。 例如，若要報告同意授權者資料庫擁有者 (`dbo`) 的所有權限，請執行下列陳述式：  
  
```  
EXEC sp_helprotect NULL, NULL, dbo;  
```  
  
 Or  
  
```  
EXEC sp_helprotect @grantorname = 'dbo';  
```  
  
 輸出報表的排序依據如下：權限類別目錄、擁有者、物件、被授與者、同意授權者、保護類型類別目錄、保護類型、動作，以及資料行循序識別碼。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
 傳回的資訊受限於中繼資料存取限制。 主體對其沒有權限的實體不會出現。  如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-the-permissions-for-a-table"></a>A. 列出資料表的權限  
 下列範例會列出 `titles` 資料表的權限。  
  
```  
EXEC sp_helprotect 'titles';  
```  
  
### <a name="b-listing-the-permissions-for-a-user"></a>B. 列出使用者的權限  
 下列範例會列出使用者 `Judy` 在目前資料庫中擁有的所有權限。  
  
```  
EXEC sp_helprotect NULL, 'Judy';  
```  
  
### <a name="c-listing-the-permissions-granted-by-a-specific-user"></a>C. 列出特定使用者授與的權限  
 下列範例會列出使用者 `Judy` 在目前資料庫中授與的所有權限，並利用 `NULL` 作為遺漏參數的預留位置。  
  
```  
EXEC sp_helprotect NULL, NULL, 'Judy';  
```  
  
### <a name="d-listing-the-statement-permissions-only"></a>D. 只列出陳述式權限  
 下列範例會列出目前資料庫中的所有陳述式權限，並利用 `NULL` 作為遺漏參數的預留位置。  
  
```  
EXEC sp_helprotect NULL, NULL, NULL, 's';   
```  
  
### <a name="e-listing-the-permissions-for-a-create-statement"></a>e. 列出 CREATE 陳述式的權限  
 下列範例會列出已獲得 CREATE TABLE 權限的所有使用者。  
  
```  
EXEC sp_helprotect @name = 'CREATE TABLE';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [拒絕 &#40;Transact-sql&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-sql&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
