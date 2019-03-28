---
title: sp_update_proxy (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 29a95b506fbbfb5342410d8d393f0091dd98834b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534460"
---
# <a name="spupdateproxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更現有 Proxy 的屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>引數  
`[ @proxy_id = ] id` 若要變更 proxy 之 proxy 識別碼。 *Proxy_id*是**int**，預設值是 NULL。  
  
`[ @proxy_name = ] 'proxy_name'` 若要變更 proxy 的名稱。 *Proxy_name*是**sysname**，預設值是 NULL。  
  
`[ @credential_name = ] 'credential_name'` Proxy 新認證的名稱。 *Credential_name*是**sysname**，預設值是 NULL。 任一*credential_name*或是*credential_id*可能指定。  
  
`[ @credential_id = ] credential_id` Proxy 新認證的識別碼。 *Credential_id*是**int**，預設值是 NULL。 任一*credential_name*或是*credential_id*可能指定。  
  
`[ @new_name = ] 'new_name'` Proxy 新的名稱。 *New_name*是**sysname**，預設值是 NULL。 當未提供，程序會變更的 proxy 名稱*new_name*。 當這個引數是 NULL 時，Proxy 的名稱會維持不變。  
  
`[ @enabled = ] is_enabled` 是 proxy 是否已啟用。 *Is_enabled&lt*旗標**tinyint**，預設值是 NULL。 當*is_enabled&lt*是**0**，proxy 未啟用，並無法供作業步驟。 當這個引數是 NULL 時，Proxy 的狀態會維持不變。  
  
`[ @description = ] 'description'` Proxy 新的描述。 *描述*是**nvarchar(512)**，預設值是 NULL。 當這個引數是 NULL 時，Proxy 的描述會維持不變。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 任一**@proxy_name**或是**@proxy_id**必須指定。 如果同時指定了兩個引數，這兩個引數都必須參考相同的 Proxy，否則，預存程序會失敗。  
  
 任一**@credential_name**或是**@credential_id**必須指定要變更 proxy 的認證。 如果同時指定了兩個引數，這兩個引數必須參考相同的認證，否則，預存程序會失敗。  
  
 這個程序會變更 Proxy，但不會變更 Proxy 的存取權。 若要變更的存取權的 proxy，使用**sp_grant_login_to_proxy**並**sp_revoke_login_from_proxy**。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的安全性角色可以執行此程序。  
  
## <a name="examples"></a>範例  
 下列範例會將 `Catalog application proxy` Proxy 的 enabled 值設為 `0`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
