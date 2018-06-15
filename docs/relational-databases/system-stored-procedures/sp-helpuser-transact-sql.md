---
title: sp_helpuser (TRANSACT-SQL) |Microsoft 文件
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
- sp_helpuser
- sp_helpuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpuser
ms.assetid: 9c70b41d-ef4c-43df-92da-bd534c287ca1
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 343439dd04f9f74c0a5444afef25921072d9d14c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261124"
---
# <a name="sphelpuser-transact-sql"></a>sp_helpuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  報告目前資料庫中資料庫層級主體的相關資訊。  
  
> [!IMPORTANT]  
>  **sp_helpuser**不會傳回中所導入的安全性實體相關的資訊[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 使用[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpuser [ [ @name_in_db = ] 'security_account' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@name_in_db =** ] **'***security_account***'**  
 這是目前資料庫中之資料庫使用者或資料庫角色的名稱。 *security_account*必須存在於目前的資料庫。 *security_account*是**sysname**，預設值是 NULL。 如果*security_account*未指定， **sp_helpuser**傳回所有的資料庫主體的相關資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 下表顯示時兩者的結果集的使用者帳戶，也不[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已為指定 Windows 使用者或*security_account*。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**UserName**|**sysname**|目前資料庫中的使用者。|  
|**RoleName**|**sysname**|角色**UserName**所屬。|  
|**LoginName**|**sysname**|登入的**UserName**。|  
|**DefDBName**|**sysname**|預設資料庫**UserName**。|  
|**DefSchemaName**|**sysname**|資料庫使用者的預設結構描述。|  
|**UserID**|**smallint**|識別碼**UserName**目前資料庫中。|  
|**SID**|**smallint**|使用者安全性識別碼 (SID)。|  
  
 下表顯示未指定使用者帳戶且別名存在於目前資料庫中時的結果集。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|作為目前資料庫中之使用者的別名之登入。|  
|**UserNameAliasedTo**|**sysname**|目前資料庫中以該登入為別名的使用者名稱。|  
  
 下表顯示的結果集為指定角色時*security_account*。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**role_name**|**sysname**|目前資料庫中角色的名稱。|  
|**Role_id**|**smallint**|目前資料庫中角色的角色識別碼。|  
|**Users_in_role**|**sysname**|目前資料庫中角色的成員。|  
|**使用者識別碼**|**smallint**|角色成員的使用者識別碼。|  
  
## <a name="remarks"></a>備註  
 若要查看資料庫角色的成員資格的相關資訊，請使用[sys.database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)。 若要查看伺服器角色成員的相關資訊，請使用[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)，並查看伺服器層級主體的相關資訊，請使用[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。  
  
 傳回的資訊受限於中繼資料存取限制。 主體對其沒有權限的實體不會出現。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-users"></a>A. 列出所有使用者  
 下列範例會列出目前資料庫中的所有使用者。  
  
```  
EXEC sp_helpuser;  
```  
  
### <a name="b-listing-information-for-a-single-user"></a>B. 列出單一使用者的資訊  
 下列範例會列出使用者資料庫擁有者 (`dbo`) 的相關資訊。  
  
```  
EXEC sp_helpuser 'dbo';  
```  
  
### <a name="c-listing-information-for-a-database-role"></a>C. 列出資料庫角色的資訊  
 下列範例會列出 `db_securityadmin` 固定資料庫角色的相關資訊。  
  
```  
EXEC sp_helpuser 'db_securityadmin';  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
  
