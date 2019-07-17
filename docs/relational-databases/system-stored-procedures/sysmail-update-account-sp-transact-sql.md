---
title: sysmail_update_account_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9ba9e1f0757f23072b5e4f18f73fb5f7c69a005a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037358"
---
# <a name="sysmailupdateaccountsp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更現有 Database Mail 帳戶中的資訊。  
 
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>引數  
`[ @account_id = ] account_id` 要更新的帳戶識別碼。 *account_id*已**int**，預設值是 NULL。 至少其中一個*account_id*或是*account_name*必須指定。 如果同時指定這兩者，程序會變更帳戶的名稱。  
  
`[ @account_name = ] 'account_name'` 要更新的帳戶名稱。 *account_name*已**sysname**，預設值是 NULL。 至少其中一個*account_id*或是*account_name*必須指定。 如果同時指定這兩者，程序會變更帳戶的名稱。  
  
`[ @email_address = ] 'email_address'` 將訊息從傳送新的電子郵件地址。 這個地址必須是網際網路電子郵件地址。 地址中的伺服器名稱是 Database Mail 用來從這個帳戶傳送郵件的伺服器。 *email_address*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** ，預設值是 NULL。  
  
`[ @display_name = ] 'display_name'` 若要使用此帳戶的電子郵件訊息上的新顯示名稱。 *display_name*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** ，沒有預設值。  
  
`[ @replyto_address = ] 'replyto_address'` 在此帳戶的電子郵件訊息回覆至 標頭中使用新的位址。 *replyto_address*已 **& lt;languagekeyword>nvarchar(128)</languagekeyword>** ，沒有預設值。  
  
`[ @description = ] 'description'` 帳戶的新描述。 *描述*已**nvarchar(256)** ，預設值是 NULL。  
  
`[ @mailserver_name = ] 'server_name'` 若要使用此帳戶的 SMTP 郵件伺服器新名稱。 執行的電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必須能夠解析*server_name*為 IP 位址。 *server_name*已**sysname**，沒有預設值。  
  
`[ @mailserver_type = ] 'server_type'` 郵件伺服器的新的類型。 *server_type*已**sysname**，沒有預設值。 值 **'SMTP'** 支援。  
  
`[ @port = ] port_number` 郵件伺服器的新連接埠號碼。 *port_number*已**int**，沒有預設值。  
  
`[ @timeout = ] 'timeout'` 之 SmtpClient.Send 的單一電子郵件訊息的逾時參數。 *逾時*已**int** （秒)，沒有預設值。  
  
`[ @username = ] 'username'` 新的使用者名稱，用以登入郵件伺服器。 *使用者名稱*已**sysname**，沒有預設值。  
  
`[ @password = ] 'password'` 要用來登入郵件伺服器的新密碼。 *密碼*已**sysname**，沒有預設值。  
  
`[ @use_default_credentials = ] use_default_credentials` 指定是否要將郵件傳送至 SMTP 伺服器使用的認證[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]服務。 **use_default_credentials** bit，沒有預設值。 當此參數是 1 時，Database Mail 會使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的認證。 此參數為 0 時，會使用 Database Mail **@username** 並 **@password** SMTP 伺服器上進行驗證。 如果 **@username** 並 **@password** 是 NULL，則它會使用匿名驗證。 在指定此參數之前，請洽 SMTP 管理員。  
  
`[ @enable_ssl = ] enable_ssl` 指定 Database Mail 是否加密使用 Secure Sockets Layer (SSL) 通訊。 如果 SMTP 伺服器上需要 SSL，則使用此選項。 **enable_ssl** bit，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 當同時指定帳戶名稱和帳戶識別碼時，除了更新帳戶資訊之外，預存程序還會變更帳戶名稱。 在更正帳戶名稱的錯誤時，變更帳戶名稱可能會很有用。  
  
 預存程序**sysmail_update_account_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-information-for-an-account"></a>A. 變更帳戶的資訊  
 下列範例會更新帳戶`AdventureWorks Administrator`中**msdb**資料庫。 帳戶資訊設成所提供的值。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. 變更帳戶名稱和帳戶資訊  
 下列範例會利用帳戶識別碼 `125` 來變更名稱及更新帳戶資訊。 帳戶的新名稱是 `Backup Mail Server`。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
