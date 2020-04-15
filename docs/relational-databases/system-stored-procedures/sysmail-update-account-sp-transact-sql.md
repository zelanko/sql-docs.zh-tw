---
title: sysmail_update_account_sp(轉算-SQL) |微軟文件
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
ms.openlocfilehash: 3dd772a1519ea856cac0302d31be9eb7d0f9d782
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283134"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
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
`[ @account_id = ] account_id`要更新的帳戶 ID。 *account_id* **為 int,** 預設值為 NULL。 必須至少指定一個*account_id*或*account_name。* 如果同時指定這兩者，程序會變更帳戶的名稱。  
  
`[ @account_name = ] 'account_name'`要更新的帳戶的名稱。 *account_name*是**sysname,** 預設值為 NULL。 必須至少指定一個*account_id*或*account_name。* 如果同時指定這兩者，程序會變更帳戶的名稱。  
  
`[ @email_address = ] 'email_address'`要從中發送消息的新電子郵寄地址。 這個地址必須是網際網路電子郵件地址。 地址中的伺服器名稱是 Database Mail 用來從這個帳戶傳送郵件的伺服器。 *email_address*是**nvarchar (128),** 預設值為 NULL。  
  
`[ @display_name = ] 'display_name'`要用於此帳戶的電子郵件的新顯示名稱。 *display_name*是**nvarchar(128),** 沒有預設值。  
  
`[ @replyto_address = ] 'replyto_address'`要在此帳戶的電子郵件的回復-To 標頭中使用的新位址。 *replyto_address*是**nvarchar(128),** 沒有預設值。  
  
`[ @description = ] 'description'`帳戶的新說明。 *描述*是**nvarchar (256),** 預設值為 NULL。  
  
`[ @mailserver_name = ] 'server_name'`用於此帳戶的 SMTP 郵件伺服器的新名稱。 運行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的電腦必須能夠解析*server_name*到 IP 位址。 *server_name*是**系統名稱**,沒有預設值。  
  
`[ @mailserver_type = ] 'server_type'`郵件伺服器的新類型。 *server_type*是**系統名稱**,沒有預設值。 僅支援 **「SMTP」** 的值。  
  
`[ @port = ] port_number`郵件伺服器的新埠號。 *port_number* **為 int,** 沒有預設值。  
  
`[ @timeout = ] 'timeout'`SmtpClient.發送單個電子郵件的超時參數。 *超時***以秒**為單位,沒有預設值。  
  
`[ @username = ] 'username'`用於登錄到郵件伺服器的新使用者名稱。 *使用者名稱*是**系統名稱**,沒有預設值。  
  
`[ @password = ] 'password'`用於登錄到郵件伺服器的新密碼。 *密碼*是**sysname,** 沒有預設值。  
  
`[ @use_default_credentials = ] use_default_credentials`指定是否使用[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]服務的認證將郵件發送到 SMTP 伺服器。 **use_default_credentials**位,沒有預設值。 當此參數是 1 時，Database Mail 會使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的認證。 當此參數為 0 時**\@**,資料庫郵件使用**\@使用者名和密碼**在 SMTP 伺服器上進行身份驗證。 如果**\@使用者名和密碼****\@為**NULL,則它將使用匿名身份驗證。 在指定此參數之前，請洽 SMTP 管理員。  
  
`[ @enable_ssl = ] enable_ssl`指定資料庫郵件是否使用傳輸層安全 (TLS)加密通訊,以前稱為安全套接字層 (SSL)。 如果您的 SMTP 伺服器上需要 TLS,請使用此選項。 **enable_ssl**位,沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0(** 成功 )或**1(** 失敗 )  
  
## <a name="remarks"></a>備註  
 當同時指定帳戶名稱和帳戶識別碼時，除了更新帳戶資訊之外，預存程序還會變更帳戶名稱。 在更正帳戶名稱的錯誤時，變更帳戶名稱可能會很有用。  
  
 儲存過程**sysmail_update_account_sp**位於**msdb**資料庫中,由**dbo**架構所有。 如果目前資料庫不是**msdb,** 則必須使用三部分名稱執行該過程。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員**固定伺服器角色的成員身份。  
  
## <a name="examples"></a>範例  
  
### <a name="a-changing-the-information-for-an-account"></a>A. 變更帳戶的資訊  
 下面的範例更新`AdventureWorks Administrator`**msdb**資料庫中的帳戶。 帳戶資訊設成所提供的值。  
  
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
 [資料庫郵件](../../relational-databases/database-mail/database-mail.md)   
 [建立資料庫郵件帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [資料庫郵件儲存過程&#40;處理-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
