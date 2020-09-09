---
description: sp_droprole (Transact-SQL)
title: sp_droprole (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6180676b4458a5f270f9ecab9bb35d2ed8a481c4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548083"
---
# <a name="sp_droprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  從目前資料庫移除資料庫角色。  
  
> [!IMPORTANT]  
>  在中 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ， **sp_droprole** 已被 DROP ROLE 語句取代。 **sp_droprole** 僅隨附于與舊版相容 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，未來版本可能不支援。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>引數  
`[ @rolename = ] 'role'` 這是要從目前資料庫中移除的資料庫角色名稱。 *role* 是 **sysname**，沒有預設值。 *角色* 必須已存在於目前的資料庫中。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 您只能使用 **sp_droprole**來移除資料庫角色。  
  
 無法移除含現有成員的資料庫角色。 資料庫角色的所有成員，都必須在移除資料庫角色之前移除。 若要從角色移除使用者，請使用 **sp_droprolemember**。 如果有任何使用者仍然是角色的成員， **sp_droprole** 會顯示這些成員。  
  
 固定角色和 **公用** 角色無法移除。  
  
 如果角色擁有任何安全性實體，就不能移除。 在卸除擁有安全性實體的應用程式角色之前，必須先傳送或卸除安全性實體的擁有權。 請使用 ALTER AUTHORIZATION 來變更不能移除之物件的擁有者。  
  
 **sp_droprole** 無法在使用者自訂交易內執行。  
  
## <a name="permissions"></a>權限  
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
 [sp_dropapprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
