---
title: sysmail_add_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b00e0eed5a27c9d795de027f82b01763c44ab80e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63472120"
---
# <a name="sysmailaddprofilesp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立新的 Database Mail 設定檔。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_name = ] 'profile\_name'` 新的設定檔的名稱。 *profile_name*已**sysname**，沒有預設值。  
  
`[ @description = ] 'description'` 新的設定檔的選擇性描述。 *描述*已**nvarchar(256)** ，沒有預設值。  
  
`[ @profile_id = ] _new\_profile\_idOUTPUT` 傳回新的設定檔的識別碼。 *new_profile_id*已**int**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 Database Mail 設定檔會保存任意數目的 Database Mail 帳戶。 Database Mail 預存程序可以利用這個程序所產生的設定檔名稱或設定檔識別碼來參考設定檔。 如需有關將帳戶新增至設定檔的詳細資訊，請參閱 < [sysmail_add_profileaccount_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)。  
  
 預存程序，則可以變更設定檔名稱和描述**sysmail_update_profile_sp**，而這個設定檔識別碼維持不變的存留期間的設定檔。  
  
 Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的設定檔名稱必須是唯一的，否則，預存程序會傳回一則錯誤。  
  
 預存程序**sysmail_add_profile_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 **A.建立新的設定檔**  
  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的新 Database Mail 設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B.建立新的設定檔，將設定檔識別碼儲存在變數中**  
  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的新 Database Mail 設定檔。 這個範例會將設定檔識別碼儲存在 `@profileId` 變數中，且會傳回包含新設定檔之設定檔識別碼的結果集。  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
