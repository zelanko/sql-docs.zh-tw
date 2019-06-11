---
title: sp_enum_login_for_proxy (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
ms.author: vanto
author: VanMSFT
manager: jroth
ms.openlocfilehash: fd5b172b7029376d6f9641552315fc64e734cc8a
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822635"
---
# <a name="spenumloginforproxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出安全性主體和 Proxy 之間的關聯。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'name'` 名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主體、 登入、 伺服器角色或**msdb**要列出 proxy 的資料庫角色。 檔案名**nvarchar(256)** ，預設值是 NULL。  
  
`[ @proxy_id = ] id` 要列出資訊的 proxy 之 proxy 識別碼。 *Proxy_id*是**int**，預設值是 NULL。 任一*識別碼*或*proxy_name*可能指定。  
  
`[ @proxy_name = ] 'proxy_name'` 要列出資訊的 proxy 名稱。 *Proxy_name*是**sysname**，預設值是 NULL。 任一*識別碼*或*proxy_name*可能指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Proxy 識別碼。|  
|**proxy_name**|**sysname**|Proxy 的名稱。|  
|**name**|**sysname**|關聯的安全性主體名稱。|  
|**flags**|**int**|安全性主體的類型。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入<br /><br /> **1** = 固定的系統角色<br /><br /> **2** = 資料庫角色中的**msdb**|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="remarks"></a>備註  
 當未不提供任何參數時， **sp_enum_login_for_proxy**列出每個 proxy 執行個體中的所有登入資訊。  
  
 當提供 proxy 識別碼或 proxy 名稱時， **sp_enum_login_for_proxy**列出有權存取 proxy 的登入。 提供登入名稱時， **sp_enum_login_for_proxy**登入具有 proxy 的存取權的清單。  
  
 當同時提供 Proxy 資訊和登入名稱時，如果指定的登入有權存取指定的 Proxy，結果集會傳回一個資料列。  
  
 這個預存程序位於**msdb**。  
  
## <a name="permissions"></a>Permissions  
 此程序預設值，成員的執行權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-associations"></a>A. 列出所有關聯  
 下列範例會列出在目前的執行個體中，在登入和 Proxy 之間所建立的所有權限。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. 列出特定登入的 Proxy  
 下列範例會列出登入 `terrid` 有權存取的 Proxy。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_help_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
