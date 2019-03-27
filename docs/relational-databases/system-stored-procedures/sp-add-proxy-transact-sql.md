---
title: sp_add_proxy (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 247c834abfbc47485628702bf4cd87c7662c44a8
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494270"
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @proxy_name = ] 'proxy_name'` 若要建立 proxy 的名稱。 *Proxy_name*是**sysname**，預設值是 NULL。 當*proxy_name*為 NULL 或空字串，則 proxy 會預設為名稱*user_name*提供。  
  
`[ @enabled = ] is_enabled` 指定是否啟用 proxy。 *Is_enabled&lt*旗標**tinyint**，預設值是 1。 當*is_enabled&lt*是**0**，proxy 未啟用，並無法供作業步驟。  
  
`[ @description = ] 'description'` Proxy 的描述。 描述**nvarchar(512)**，預設值是 NULL。 您可以利用這項描述來建立 Proxy 的文件，但並不供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用。 因此，這個引數是選擇性的。  
  
`[ @credential_name = ] 'credential_name'` Proxy 認證的名稱。 *Credential_name*是**sysname**，預設值是 NULL。 任一*credential_name*或是*credential_id*必須指定。  
  
`[ @credential_id = ] credential_id` Proxy 的認證識別碼。 *Credential_id*是**int**，預設值是 NULL。 任一*credential_name*或是*credential_id*必須指定。  
  
`[ @proxy_id = ] id OUTPUT` 如果成功建立指派給 proxy 之 proxy 識別碼。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 這個預存程序都必須執行**msdb**資料庫。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 會管理包含非 [!INCLUDE[tsql](../../includes/tsql-md.md)] 子系統之作業步驟的安全性。 每個 Proxy 都對應於一個安全性認證。 Proxy 可能會有任意數目之子系統的存取權。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的安全性角色可以執行此程序。  
  
 成員**sysadmin**固定的安全性角色，可建立使用任何 proxy 的作業步驟。 使用預存程序[sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)授與其他登入存取的 proxy。  
  
## <a name="examples"></a>範例  
 這個範例會建立 `CatalogApplicationCredential` 認證的 Proxy。 程式碼假設認證已經存在。 如需有關認證的詳細資訊，請參閱 < [CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)。  
  
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
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
