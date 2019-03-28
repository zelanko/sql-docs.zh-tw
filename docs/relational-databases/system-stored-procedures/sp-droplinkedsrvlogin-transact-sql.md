---
title: sp_droplinkedsrvlogin (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 505e75dfab9ea4e2ba44d8ef12f0ba5c7eecbde2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533510"
---
# <a name="spdroplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之本機伺服器的登入與連結伺服器的登入之間的現有對應。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>引數  
`[ @rmtsrvname = ] 'rmtsrvname'` 連結的伺服器名稱，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入對應所套用。 *rmtsrvname&lt*已**sysname**，沒有預設值。 *rmtsrvname&lt*必須已經存在。  
  
`[ @locallogin = ] 'locallogin'` 已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是對應至連結伺服器的本機伺服器登入*rmtsrvname&lt*。 *locallogin*已**sysname**，沒有預設值。 對應*locallogin*要*rmtsrvname&lt*必須已經存在。 如果是 NULL，所建立的預設對應**sp_addlinkedserver**，它會對應至登入連結的伺服器上的本機伺服器上的所有登入已刪除。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 在本機伺服器時的現有對應刪除登入後，使用所建立的預設對應**sp_addlinkedserver**當它連接至連結的伺服器代表該登入。 若要變更預設對應，請使用**sp_addlinkedsrvlogin**。  
  
 如果也會刪除預設對應，僅有明確獲得登入對應至連結的伺服器，使用的登入**sp_addlinkedsrvlogin**，連結的伺服器可以存取。  
  
 **sp_droplinkedsrvlogin**無法從使用者定義交易內執行。  
  
## <a name="permissions"></a>Permissions  
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
  
  
