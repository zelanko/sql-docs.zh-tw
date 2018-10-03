---
title: sp_droprole (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77c642d6b1574006122af74f0538cdb7ef607535
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620806"
---
# <a name="spdroprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除資料庫角色。  
  
> [!IMPORTANT]  
>  在  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_droprole**已經被 DROP ROLE 陳述式所取代。 **sp_droprole**碼只是為了與舊版的相容性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不一定支援未來的版本。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>引數  
 [  **@rolename =** ] **'***角色***'**  
 這是要從目前資料庫移除的資料庫角色名稱。 *角色*已**sysname**，沒有預設值。 *角色*必須已存在於目前的資料庫。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 只有資料庫角色可以使用來移除**sp_droprole**。  
  
 無法移除含現有成員的資料庫角色。 資料庫角色的所有成員，都必須在移除資料庫角色之前移除。 若要從角色移除使用者，請使用**sp_droprolemember**。 如果任何使用者仍角色的成員， **sp_droprole**會顯示這些成員。  
  
 固定角色和**公開**角色不能移除。  
  
 如果角色擁有任何安全性實體，就不能移除。 在卸除擁有安全性實體的應用程式角色之前，必須先傳送或卸除安全性實體的擁有權。 請使用 ALTER AUTHORIZATION 來變更不能移除之物件的擁有者。  
  
 **sp_droprole**無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>Permissions  
 需要角色的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 下列範例會移除應用程式角色 `Sales`。  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_dropapprole &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
