---
title: sp_helprotect (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8f98f62b10b38d726feec2bd427bc7d1fc6dcea9
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534500"
---
# <a name="sphelprotect-transact-sql"></a>sp_helprotect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回報表，報表中有目前資料庫中之物件的使用者權限或陳述式權限的相關資訊。  
  
> [!IMPORTANT]  
>  **sp_helprotect**不會傳回所導入之安全性實體相關的資訊[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 使用[sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)並[fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)改。  
  
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
`[ @name = ] 'object_statement'` 是在目前資料庫中，或是具有報表的權限的陳述式，物件的名稱。 *object_statement&lt*已**nvarchar(776)**，預設值是 NULL，它會傳回所有物件和陳述式的權限。 如果值是物件 (資料表、檢視、預存程序或擴充預存程序)，它必須是目前資料庫中的有效物件。 物件名稱可以在表單中包含的擁有者限定詞_擁有者_**。**_物件_。  
  
 如果*object_statement&lt*是陳述式，它可以是 CREATE 陳述式。  
  
`[ @username = ] 'security_account'` 是為其傳回的權限名稱。 *security_account*已**sysname**，預設值是 NULL，它會傳回所有主體目前資料庫中。 *security_account*必須存在於目前的資料庫。  
  
`[ @grantorname = ] 'grantor'` 是授與權限名稱。 *另外，grantor*已**sysname**，預設值是 NULL，它會傳回資料庫中任何主體授與的權限的所有資訊。  
  
`[ @permissionarea = ] 'type'` 這是字元字串，指出是否要顯示物件的權限 (字元字串**o**)，陳述式權限 (字元字串**s**)，或兩者 (**os**)。 *型別*已**varchar(10)**，預設值是**os**。 *型別*可以是任意的組合**o**並**s**，不論有無逗號或空格之間**o**並**s**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**[擁有者]**|**sysname**|物件擁有者的名稱。|  
|**物件**|**sysname**|物件的名稱。|  
|**被授與者**|**sysname**|對其授與權限之主體的名稱。|  
|**授與者**|**sysname**|對指定的被授與者授與權限之主體的名稱。|  
|**ProtectType**|**nvarchar(10)**|保護類型的名稱：<br /><br /> GRANT REVOKE|  
|**動作**|**nvarchar(60)**|權限的名稱。 權限陳述式是否有效，需根據物件類型而定。|  
|**資料行**|**sysname**|權限的類型：<br /><br /> 全部 = 權限涵蓋物件的所有目前資料行。<br /><br /> 新增 = 權限涵蓋未來可能在物件上變更 (利用 ALTER 陳述式) 的任何新資料行。<br /><br /> 全部+新增 = 全部和新增的組合。<br /><br /> 如果權限類型不適用於資料行，則傳回句號。|  
  
## <a name="remarks"></a>備註  
 下列程序中的所有參數都是選擇性的。 如果執行時沒有設定任何參數，則 `sp_helprotect` 會顯示所有已在目前資料庫中授與或拒絕的權限。  
  
 如果只指定了部份 (而非全部) 參數，請利用具名參數來識別特定參數，或識別作為預留位置的 `NULL`。 例如，若要報告同意授權者資料庫擁有者 (`dbo`) 的所有權限，請執行下列陳述式：  
  
```  
EXEC sp_helprotect NULL, NULL, dbo;  
```  
  
 或  
  
```  
EXEC sp_helprotect @grantorname = 'dbo';  
```  
  
 輸出報表的排序依據如下：權限類別目錄、擁有者、物件、被授與者、同意授權者、保護類型類別目錄、保護類型、動作，以及資料行循序識別碼。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
 傳回的資訊受限於中繼資料存取限制。 主體對其沒有權限的實體不會出現。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
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
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
