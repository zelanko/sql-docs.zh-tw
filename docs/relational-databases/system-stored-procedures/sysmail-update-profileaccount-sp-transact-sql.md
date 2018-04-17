---
title: sysmail_update_profileaccount_sp (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b005301a0fa1b7dcfc7cd2c5c27ccdce565fb8dc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailupdateprofileaccountsp-transact-sql"></a>sysmail_update_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新 Database Mail 設定檔內的帳戶序號。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>引數  
 [ **@profile_id** =] *profile_id*  
 要更新之設定檔的設定檔識別碼。 *profile_id*是**int**，預設值是 NULL。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 要更新之設定檔的設定檔名稱。 *profile_name*是**sysname**，預設值是 NULL。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@account_id** = ] *account_id*  
 這是要更新的帳戶識別碼。 *account_id*是**int**，預設值是 NULL。 任一*account_id*或*account_name*必須指定。  
  
 [ **@account_name** = ] **'***account_name***'**  
 這是要更新的帳戶名稱。 *account_name*是**sysname**，預設值是 NULL。 任一*account_id*或*account_name*必須指定。  
  
 [ **@sequence_number** = ] *sequence_number*  
 帳戶的新序號。 *sequence_number*是**int**，沒有預設值。 序號決定了帳戶在設定檔中的使用順序。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 如果指定的帳戶與指定的設定檔無關，便會傳回一則錯誤。  
  
 序號決定了 Database Mail 使用設定檔中之帳戶的順序。 如果是新的電子郵件訊息，Database Mail 會從序號最低的帳戶開始。 如果這個帳戶失敗，Database Mail 會使用序號次高的帳戶，依此類推，直到 Database Mail 傳送訊息成功為止，或直到序號最高的帳戶失敗為止。 如果序號最高的帳戶失敗，電子郵件訊息也會失敗。  
  
 如果有多個序號相同的帳戶存在，Database Mail 只會將其中一個帳戶用在給定的電子郵件訊息上。 在這個情況下，Database Mail 並無法保證這個序號會用到哪個帳戶，也無法保證各訊息會用到相同的帳戶。  
  
 預存程序**sysmail_update_profileaccount_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會變更帳戶的序號`Admin-BackupServer`設定檔中`AdventureWorks Administrator`中**msdb**資料庫。 執行這個程式碼之後，帳戶的序號是 `3`，表示如果前面兩個帳戶失敗，就輪到它。  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
