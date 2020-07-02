---
title: sp_update_proxy （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 66ca1f35a5920f6f6d26bea0663e51d305fc1c3b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775153"
---
# <a name="sp_update_proxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

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
`[ @proxy_id = ] id`要變更之 proxy 的 proxy 識別碼。 *Proxy_id*是**int**，預設值是 Null。  
  
`[ @proxy_name = ] 'proxy_name'`要變更之 proxy 的名稱。 *Proxy_name*是**sysname**，預設值是 Null。  
  
`[ @credential_name = ] 'credential_name'`Proxy 的新認證名稱。 *Credential_name*是**sysname**，預設值是 Null。 可以指定*credential_name*或*credential_id* 。  
  
`[ @credential_id = ] credential_id`Proxy 的新認證識別碼。 *Credential_id*是**int**，預設值是 Null。 可以指定*credential_name*或*credential_id* 。  
  
`[ @new_name = ] 'new_name'`Proxy 的新名稱。 *New_name*是**sysname**，預設值是 Null。 當提供時，程式會將 proxy 的名稱變更為*new_name*。 當這個引數是 NULL 時，Proxy 的名稱會維持不變。  
  
`[ @enabled = ] is_enabled`這是指是否啟用 proxy。 *Is_enabled*旗標是**Tinyint**，預設值是 Null。 當*is_enabled*為**0**時，不會啟用 proxy，作業步驟也不能使用。 當這個引數是 NULL 時，Proxy 的狀態會維持不變。  
  
`[ @description = ] 'description'`Proxy 的新描述。 *描述*是**Nvarchar （512）**，預設值是 Null。 當這個引數是 NULL 時，Proxy 的描述會維持不變。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 必須指定** \@ proxy_name**或** \@ proxy_id** 。 如果同時指定了兩個引數，這兩個引數都必須參考相同的 Proxy，否則，預存程序會失敗。  
  
 必須指定** \@ credential_name**或** \@ credential_id** ，才能變更 proxy 的認證。 如果同時指定了兩個引數，這兩個引數必須參考相同的認證，否則，預存程序會失敗。  
  
 這個程序會變更 Proxy，但不會變更 Proxy 的存取權。 若要變更 proxy 的存取權，請使用**sp_grant_login_to_proxy**並**sp_revoke_login_from_proxy**。  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定安全性角色的成員，才能夠執行此程式。  
  
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
 [SQL Server Agent 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [實行 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
