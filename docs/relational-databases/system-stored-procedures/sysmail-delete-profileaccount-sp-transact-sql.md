---
title: sysmail_delete_profileaccount_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profileaccount_sp
- sysmail_delete_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profileaccount_sp
ms.assetid: b58d06f2-d6c9-4c8e-95bd-027c50f4621a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a999fe9c0fc6425cc4debc950c3a9da97ffdbf56
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832445"
---
# <a name="sysmail_delete_profileaccount_sp-transact-sql"></a>sysmail_delete_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從 Database Mail 設定檔中移除帳戶。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_profileaccount_sp  {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    {   [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_id = ] profile_id`要刪除之設定檔的設定檔識別碼。 *profile_id*是**int**，預設值是 Null。 可以指定*profile_id*或*profile_name* 。  
  
`[ @profile_name = ] 'profile_name'`要刪除之設定檔的設定檔名稱。 *profile_name*是**sysname**，預設值是 Null。 可以指定*profile_id*或*profile_name* 。  
  
`[ @account_id = ] account_id`要刪除的帳戶識別碼。 *account_id*是**int**，預設值是 Null。 可以指定*account_id*或*account_name* 。  
  
`[ @account_name = ] 'account_name'`要刪除的帳戶名稱。 *account_name*是**sysname**，預設值是 Null。 可以指定*account_id*或*account_name* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 如果指定的帳戶與指定的設定檔無關，便會傳回一則錯誤。  
  
 當指定了帳戶，但沒有指定設定檔時，這個預存程序會從所有設定檔中移除指定的帳戶。 例如，如果您準備關閉現有的 SMTP 伺服器，請從所有設定檔中移除使用這個 SMTP 伺服器的帳戶，而不是從每個設定檔中移除每個帳戶。  
  
 當指定了設定檔，但沒有指定帳戶時，這個預存程序會從指定的設定檔中移除所有帳戶。 例如，如果您在變更設定檔所用的 SMTP 伺服器，從設定檔中移除所有帳戶，再依照需要來加入新帳戶，可能會很方便。  
  
 預存程式**sysmail_delete_profileaccount_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱來執行此程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會顯示從 `Audit Account` 設定檔移除 `AdventureWorks Administrator` 帳戶。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 設定物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
