---
title: sp_addrole （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1711ec3941a5fced5ef9e0c32808d6153b673e2b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68030912"
---
# <a name="sp_addrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在目前資料庫中建立新的資料庫角色。  
  
> [!IMPORTANT]
>  包含**sp_addrole**以提供與舊版的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相容性，未來的版本可能不支援此功能。 請改用[CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md) 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] 'role'`這是新資料庫角色的名稱。 「*角色*」是一種**sysname**，沒有預設值。 *role*必須是有效的識別碼（ID），而且不能已存在於目前的資料庫中。  
  
`[ @ownername = ] 'owner'`這是新資料庫角色的擁有者。 *owner*是**sysname**，預設值是目前執行中的使用者。 *owner*必須是目前資料庫中的資料庫使用者或資料庫角色。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色的名稱，可以包含 1 到 128 個字元，其中包括字母、符號和數字。 資料庫角色的名稱不能：包含反斜線字元（\\）、為 Null 或空字串（**' '**）。  
  
 在您加入資料庫角色之後，請使用[sp_addrolemember &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)將主體新增至角色。 當您使用 GRANT、DENY 或 REVOKE 陳述式將權限套用至資料庫角色時，資料庫角色的成員會繼承那些權限，如同這些權限是直接套用至其帳戶。  
  
> [!NOTE]  
>  無法建立新的伺服器角色。 角色只能在資料庫層級建立。  
  
 **sp_addrole**不能在使用者自訂交易內使用。  
  
## <a name="permissions"></a>權限  
 需要資料庫的 CREATE ROLE 權限。 若要建立結構描述，就需要資料庫的 CREATE SCHEMA 權限。 如果將*擁有*者指定為使用者或群組，則需要在該使用者或群組上模擬。 如果將*擁有*者指定為角色，則需要該角色的 ALTER 許可權或該角色的成員。 如果擁有者被指定為應用程式角色，則需要該應用程式角色的 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會在目前資料庫中加入一個名叫 `Managers` 的新角色。  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
