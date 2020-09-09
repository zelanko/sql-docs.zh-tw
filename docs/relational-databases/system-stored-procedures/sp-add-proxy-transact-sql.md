---
description: sp_add_proxy (Transact-SQL)
title: sp_add_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07ab9b3525292f437a87c24aac775d7b22b30598
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536842"
---
# <a name="sp_add_proxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  加入指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>引數  
`[ @proxy_name = ] 'proxy_name'` 要建立的 proxy 名稱。 *Proxy_name*是**sysname**，預設值是 Null。 當 *proxy_name* 為 Null 或空字串時，proxy 的名稱預設為提供的 *user_name* 。  
  
`[ @enabled = ] is_enabled` 指定是否啟用 proxy。 *Is_enabled*旗標是**Tinyint**，預設值是1。 當 *is_enabled* 是 **0**時，不會啟用 proxy，作業步驟無法使用此 proxy。  
  
`[ @description = ] 'description'` Proxy 的描述。 描述是 **Nvarchar (512) **，預設值是 Null。 您可以利用這項描述來建立 Proxy 的文件，但並不供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用。 因此，這個引數是選擇性的。  
  
`[ @credential_name = ] 'credential_name'` Proxy 的認證名稱。 *Credential_name*是**sysname**，預設值是 Null。 必須指定 *credential_name* 或 *credential_id* 。  
  
`[ @credential_id = ] credential_id` Proxy 認證的識別碼。 *Credential_id*是**int**，預設值是 Null。 必須指定 *credential_name* 或 *credential_id* 。  
  
`[ @proxy_id = ] id OUTPUT` 如果成功建立，則指派給 proxy 的 proxy 識別碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 這個預存程式必須在 **msdb** 資料庫中執行。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 會管理包含非 [!INCLUDE[tsql](../../includes/tsql-md.md)] 子系統之作業步驟的安全性。 每個 Proxy 都對應於一個安全性認證。 Proxy 可能會有任意數目之子系統的存取權。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定安全性角色的成員，才能夠執行這個程式。  
  
 **系統管理員（sysadmin** ）固定安全性角色的成員可以建立使用任何 proxy 的作業步驟。 使用 [sp_grant_login_to_proxy &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md) 的預存程式，將 proxy 的其他登入存取權授與其他登入。  
  
## <a name="examples"></a>範例  
 這個範例會建立 `CatalogApplicationCredential` 認證的 Proxy。 程式碼假設認證已經存在。 如需認證的詳細資訊，請參閱 [CREATE CREDENTIAL &#40;transact-sql&#41;](../../t-sql/statements/create-credential-transact-sql.md)。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
