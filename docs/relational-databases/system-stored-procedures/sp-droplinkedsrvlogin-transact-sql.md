---
description: sp_droplinkedsrvlogin (Transact-SQL)
title: sp_droplinkedsrvlogin (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 30e4d997e79d0e66a75fdff8ea6c162ab7bf7634
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536515"
---
# <a name="sp_droplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  移除在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之本機伺服器的登入與連結伺服器的登入之間的現有對應。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>引數  
`[ @rmtsrvname = ] 'rmtsrvname'` 這是登入對應所套用的連結伺服器名稱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *rmtsrvname* 是 **sysname**，沒有預設值。 *rmtsrvname* 必須已經存在。  
  
`[ @locallogin = ] 'locallogin'` 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本機伺服器上具有連結伺服器 *rmtsrvname*對應的登入。 *locallogin* 是 **sysname**，沒有預設值。 *Locallogin*至*rmtsrvname*的對應必須已經存在。 如果是 Null，則會刪除 **sp_addlinkedserver**所建立的預設對應，將本機伺服器上的所有登入對應到連結伺服器上的登入。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 當刪除登入現有的對應時，本機伺服器會使用 **sp_addlinkedserver** 在代表該登入連接到連結伺服器時所建立的預設對應。 若要變更預設對應，請使用 **sp_addlinkedsrvlogin**。  
  
 如果預設對應也會一併刪除，則只有已明確授與連結伺服器登入對應的登入（使用 **sp_addlinkedsrvlogin**）可以存取連結的伺服器。  
  
 **sp_droplinkedsrvlogin** 無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
 需要伺服器的 ALTER ANY LOGIN 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>A. 移除現有使用者的登入對應  
 下列範例會移除從本機伺服器到連結伺服器 `Mary` 的登入 `Accounts` 對應。 因此，登入 `Mary` 會使用預設的登入對應。  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. 移除預設的登入對應  
 下列範例會移除原先在連結伺服器 `sp_addlinkedserver` 執行 `Accounts` 而建立的預設登入對應。  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
