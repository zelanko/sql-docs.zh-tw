---
title: sysmail_add_profileaccount_sp & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5f307fca906d138428fe9852752d3f718633181
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47729856"
---
# <a name="sysmailaddprofileaccountsp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將 Database Mail 帳戶加入 Database Mail 設定檔中。 執行**sysmail_add_profileaccount_sp**使用資料庫帳戶建立之後[sysmail_add_account_sp &#40;-&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)，和資料庫設定檔會透過[sysmail_add_profile_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@profile_id** =] *profile_id*  
 這是要加入帳戶的設定檔識別碼。 *profile_id*已**int**，預設值是 NULL。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 這是要加入帳戶的設定檔名稱。 *profile_name*已**sysname**，預設值是 NULL。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@account_id** = ] *account_id*  
 這是要加入至設定檔的帳戶識別碼。 *account_id*已**int**，預設值是 NULL。 任一*account_id*或*account_name*必須指定。  
  
 [ **@account_name** = ] **'***account_name***'**  
 這是要加入至設定檔的帳戶名稱。 *account_name*已**sysname**，預設值是 NULL。 任一*account_id*或*account_name*必須指定。  
  
 [ **@sequence_number** = ] *sequence_number*  
 帳戶在設定檔內的序號。 *sequence_number*已**int**，沒有預設值。 序號決定了帳戶在設定檔中的使用順序。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 設定檔和帳戶都必須存在。 否則，預存程序會傳回錯誤。  
  
 請注意，這個預存程序並不會變更已關聯於指定設定檔的帳戶序號。 如需有關如何更新帳戶序號的詳細資訊，請參閱 < [sysmail_update_profileaccount_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)。  
  
 序號決定了 Database Mail 使用設定檔中之帳戶的順序。 如果是新的電子郵件訊息，Database Mail 會從序號最低的帳戶開始。 如果這個帳戶失敗，Database Mail 會使用序號次高的帳戶，依此類推，直到 Database Mail 傳送訊息成功為止，或直到序號最高的帳戶失敗為止。 如果序號最高的帳戶失敗，Database Mail 會在 *sysmail_configure_sp* 的 **AccountRetryDelay**參數所設定的時間之內，暫停傳送郵件，之後，再從最低的序號開始，重新嘗試傳送郵件的處理序。 請利用 *sysmail_configure_sp* 的 **AccountRetryAttempts**參數，設定外部郵件處理序嘗試利用指定設定檔中的每個帳戶，來傳送電子郵件訊息的次數。  
  
 如果有多個序號相同的帳戶存在，Database Mail 只會將其中一個帳戶用在給定的電子郵件訊息上。 在這個情況下，Database Mail 並無法保證這個序號會用到哪個帳戶，也無法保證各訊息會用到相同的帳戶。  
  
 預存程序**sysmail_add_profileaccount_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會將 `AdventureWorks Administrator` 設定檔關聯於 `Audit Account` 帳戶。 稽核帳戶的序號是 1。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
