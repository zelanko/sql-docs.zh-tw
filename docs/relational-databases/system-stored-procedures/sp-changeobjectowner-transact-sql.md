---
description: sp_changeobjectowner (Transact-SQL)
title: sp_changeobjectowner (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e96c93be7b21deb0966e0a48f5fde3258501ac6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464420"
---
# <a name="sp_changeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  變更目前資料庫中的物件擁有者。  
  
> [!IMPORTANT]
>  這個預存程式只適用于中提供的物件 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) 或 [alter AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) 。 **sp_changeobjectowner** 變更架構和擁有者。 為了保留與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的相容性，當目前擁有者和新擁有者同時擁有與資料庫使用者同名的結構描述時，這個預存程序只會變更物件擁有者。  
> 
> [!IMPORTANT]
>  新的權限需求已經加入這個預存程序中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>引數  
`[ @objname = ] 'object'` 這是目前資料庫中現有資料表、視圖、使用者自訂函數或預存程式的名稱。 *物件* 是 **Nvarchar (776) **，沒有預設值。 *物件*可以使用現有物件的擁有者來限定，格式為_existing_owner_**。** 如果架構及其擁有者具有相同的名稱，則為_物件_。  
  
`[ @newowner = ] 'owner_ '` 這是將成為物件新擁有者的安全性帳戶名稱。 *owner* 是 **sysname**，沒有預設值。 *擁有* 者必須是有效的資料庫使用者、伺服器角色、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] windows 登入或 windows 群組，而且具有目前資料庫的存取權。 如果新擁有者是一個 Windows 使用者或是沒有對應資料庫層級主體的 Windows 群組，就會建立一個資料庫使用者。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 **sp_changeobjectowner** 從物件移除所有現有的許可權。 您必須重新套用您想要在執行 **sp_changeobjectowner**後保留的任何許可權。 因此，建議您先編寫現有許可權的腳本，再執行 **sp_changeobjectowner**。 待物件擁有權變更之後，您就可以利用指令碼，重新套用權限了。 在執行之前，您必須先修改權限指令碼中的物件擁有者。  
  
 若要變更安全性實體的擁有者，請使用 ALTER AUTHORIZATION。 若要變更結構描述，請使用 ALTER SCHEMA。  
  
## <a name="permissions"></a>權限  
 需要 **db_owner** 固定資料庫角色中的成員資格，或是 **db_ddladmin** 固定資料庫角色和 **db_securityadmin** 固定資料庫角色中的成員資格，以及物件的 CONTROL 許可權。  
  
## <a name="examples"></a>範例  
 下列範例會將資料表的擁有者變更 `authors` 為 `Corporate\GeorgeW` 。  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
