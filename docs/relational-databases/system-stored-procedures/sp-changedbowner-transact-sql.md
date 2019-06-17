---
title: sp_changedbowner (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changedbowner
- sp_changedbowner_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changedbowner
ms.assetid: 516ef311-e83b-45c9-b9cd-0e0641774c04
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1a38be84e5f1980b680d674e1c04c2ba95d1a537
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62994240"
---
# <a name="spchangedbowner-transact-sql"></a>sp_changedbowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更目前資料庫的擁有者。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_changedbowner [ @loginame = ] 'login'  
     [ , [ @map = ] remap_alias_flag ]  
```  
  
## <a name="arguments"></a>引數  
 [ @loginame= ] '*login*'  
 這是目前資料庫新擁有者的登入識別碼。 *登入*已**sysname**，沒有預設值。 *登入*必須是現有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或 Windows 使用者。 *登入*不能成為目前資料庫的擁有者，如果它已經透過資料庫中現有的使用者安全性帳戶資料庫的存取權。 若要防止這種情況，請先卸除目前資料庫的使用者。  
  
 [ @map= ] *remap_alias_flag*  
 *Remap_alias_flag*參數已被取代，因為登入別名已移除了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 使用*remap_alias_flag*參數不會產生錯誤，但是沒有任何作用。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 在 sp_changedbowner 執行之後，新擁有者在資料庫中就成為 dbo 使用者。 dbo 具有隱含權限，可以執行資料庫中所有的活動。  
  
 master、model 或 tempdb 系統資料庫的擁有者不能變更。  
  
 若要顯示一份有效*登入*值，執行 sp_helplogins 預存程序。  
  
 執行時只搭配 sp_changedbowner*登入*參數變更資料庫擁有權轉移給*登入*。  
  
 不過，您也可以利用 ALTER AUTHORIZATION 陳述式來變更任何安全性實體的擁有者。 如需詳細資訊，請參閱 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 TAKE OWNERSHIP 權限。 如果新擁有者在資料庫有對應的使用者，則需要登入的 IMPERSONATE 權限，否則就需要伺服器的 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會讓登入 `Albert` 成為目前資料庫的擁有者。  
  
```  
EXEC sp_changedbowner 'Albert';  
```  
  
## <a name="see-also"></a>另請參閱  
 [安全性預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sp_dropalias &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropalias-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helplogins &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
