---
title: "sp_enum_login_for_proxy (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs: TSQL
helpviewer_keywords: sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3c19ebb2104500b3d394a10cabb8589bc4ded0b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
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
 [  **@name** =] '*名稱*'  
 名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主體、 登入、 伺服器角色或**msdb**要列出 proxy 的資料庫角色。 名稱是**nvarchar （256)**，預設值是 NULL。  
  
 [  **@proxy_id** =]*識別碼*  
 要列出資訊的 Proxy 之 Proxy 識別碼。 *Proxy_id*是**int**，預設值是 NULL。 任一*識別碼*或*proxy_name*可指定。  
  
 [  **@proxy_name** =] **'***proxy_name***'**  
 要列出資訊的 Proxy 名稱。 *Proxy_name*是**sysname**，預設值是 NULL。 任一*識別碼*或*proxy_name*可指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|Proxy 識別碼。|  
|**proxy_name**|**sysname**|Proxy 的名稱。|  
|**name**|**sysname**|關聯的安全性主體名稱。|  
|**旗標**|**int**|安全性主體的類型。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入<br /><br /> **1** = 固定的系統角色<br /><br /> **2** = 資料庫角色中的**msdb**|  
  
## <a name="remarks"></a>備註  
 當未不提供任何參數時， **sp_enum_login_for_proxy**列出每個 proxy 執行個體中的所有登入資訊。  
  
 當提供 proxy 識別碼或 proxy 名稱時， **sp_enum_login_for_proxy**列出有權存取 proxy 的登入。 當提供登入名稱時， **sp_enum_login_for_proxy**登入的 proxy 存取權的清單。  
  
 當同時提供 Proxy 資訊和登入名稱時，如果指定的登入有權存取指定的 Proxy，結果集會傳回一個資料列。  
  
 這個預存程序位於**msdb**。  
  
## <a name="permissions"></a>Permissions  
 這個成員的程序預設值的執行權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-all-associations"></a>A. 列出所有關聯  
 下列範例會列出在目前的執行個體中，在登入和 Proxy 之間所建立的所有權限。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. 列出特定登入的 Proxy  
 下列範例會列出登入 `terrid` 有權存取的 Proxy。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>請參閱  
 [sp_help_proxy &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
