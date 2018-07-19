---
title: sp_revoke_login_from_proxy (TRANSACT-SQL) |Microsoft 文件
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
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6275facb81f14269eca19979c115c5ea80844563
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33253547"
---
# <a name="sprevokeloginfromproxy-transact-sql"></a>sp_revoke_login_from_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除安全性主體的 Proxy 存取權。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>引數  
 [ **@name=** ] **'***name***'**  
 名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入、 伺服器角色或**msdb**来移除存取權的資料庫角色。 *名稱*是**nvarchar （256)** 沒有預設值。  
  
 [ **@proxy_id=** ] *id*  
 要移除存取權之 Proxy 的識別碼。 任一*識別碼*或*proxy_name*必須指定，但不可同時指定兩者。 *識別碼*是**int**，預設值是 NULL。  
  
 [ **@proxy_name=** ] **'***proxy_name***'**  
 要移除存取權之 Proxy 的名稱。 任一*識別碼*或*proxy_name*必須指定，但不可同時指定兩者。 *Proxy_name*是**sysname**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 將無法執行參考這個 Proxy 的登入所擁有的作業。  
  
## <a name="permissions"></a>Permissions  
 若要執行這個預存程序，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會撤銷 `terrid` 這項登入存取 `Catalog application proxy` 這個 Proxy 的權利。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Agent 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_help_proxy &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
