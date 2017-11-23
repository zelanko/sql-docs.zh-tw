---
title: "sysmail_delete_profileaccount_sp (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profileaccount_sp
- sysmail_delete_profileaccount_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_delete_profileaccount_sp
ms.assetid: b58d06f2-d6c9-4c8e-95bd-027c50f4621a
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c1f60356209a9f39d0ac902fea41b5f6ec2f2a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysmaildeleteprofileaccountsp-transact-sql"></a>sysmail_delete_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從 Database Mail 設定檔中移除帳戶。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_profileaccount_sp  {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    {   [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
```  
  
## <a name="arguments"></a>引數  
 [  **@profile_id**  =] *profile_id*  
 要刪除之設定檔的設定檔識別碼。 *profile_id*是**int**，預設值是 NULL。 任一*profile_id*或*profile_name*可指定。  
  
 [  **@profile_name**  =] **'***profile_name***'**  
 要刪除之設定檔的設定檔名稱。 *profile_name*是**sysname**，預設值是 NULL。 任一*profile_id*或*profile_name*可指定。  
  
 [  **@account_id**  =] *account_id*  
 要刪除的帳戶識別碼。 *account_id*是**int**，預設值是 NULL。 任一*account_id*或*account_name*可指定。  
  
 [  **@account_name**  =] **'***account_name***'**  
 要刪除的帳戶名稱。 *account_name*是**sysname**，預設值是 NULL。 任一*account_id*或*account_name*可指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 如果指定的帳戶與指定的設定檔無關，便會傳回一則錯誤。  
  
 當指定了帳戶，但沒有指定設定檔時，這個預存程序會從所有設定檔中移除指定的帳戶。 例如，如果您準備關閉現有的 SMTP 伺服器，請從所有設定檔中移除使用這個 SMTP 伺服器的帳戶，而不是從每個設定檔中移除每個帳戶。  
  
 當指定了設定檔，但沒有指定帳戶時，這個預存程序會從指定的設定檔中移除所有帳戶。 例如，如果您在變更設定檔所用的 SMTP 伺服器，從設定檔中移除所有帳戶，再依照需要來加入新帳戶，可能會很方便。  
  
 預存程序**sysmail_delete_profileaccount_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會顯示從 `Audit Account` 設定檔移除 `AdventureWorks Administrator` 帳戶。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account' ;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
