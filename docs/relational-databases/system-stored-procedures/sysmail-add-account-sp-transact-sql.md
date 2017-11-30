---
title: "sysmail_add_account_sp (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
caps.latest.revision: "40"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e24d90b20c91ab6dfb510faad46ceb2b5f8cc19b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailaddaccountsp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立新的 Database Mail 帳戶來保留 SMTP 帳戶的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@account_name**  =] **'***account_name***'**  
 這是要加入的帳戶名稱。 *account_name*是**sysname**，沒有預設值。  
  
 [  **@email_address**  =] **'***email_address***'**  
 傳送訊息的來源電子郵件地址。 這個地址必須是網際網路電子郵件地址。 *email_address*是**nvarchar （128)**，沒有預設值。 例如，帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式可能傳送電子郵件地址從 **SqlAgent@Adventure-Works.com** 。  
  
 [  **@display_name**  =] **'***display_name***'**  
 這個帳戶發出的電子郵件訊息所用的顯示名稱。 *display_name*是**nvarchar （128)**，預設值是 NULL。 例如，帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式顯示的名稱可能**SQL Server Agent Automated Mailer**電子郵件訊息上。  
  
 [  **@replyto_address**  =] **'***replyto_address***'**  
 這是在回應此帳戶的訊息時，回應的傳送地址。 *replyto_address*是**nvarchar （128)**，預設值是 NULL。 例如，回覆給帳戶[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式可能會移至資料庫管理員，  **danw@Adventure-Works.com** 。  
  
 [  **@description**  =] **'***描述***'**  
 這是帳戶的描述。 *描述*是**nvarchar （256)**，預設值是 NULL。  
  
 [  **@mailserver_name**  =] **'***server_name***'**  
 這個帳戶要用的 SMTP 郵件伺服器的名稱或 IP 位址。 執行的電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必須能夠解析*server_name*為 IP 位址。 *server_name*是**sysname**，沒有預設值。  
  
 [  **@mailserver_type**  =] '*server_type*'  
 電子郵件伺服器的類型。 *server_type*是**sysname**，預設值是**'SMTP'**...  
  
 [  **@port**  =] *port_number*  
 電子郵件伺服器的通訊埠編號。 *port_number*是**int**，預設值為 25。  
  
 [  **@username**  =] **'***username***'**  
 用來登入電子郵件伺服器的使用者名稱。 *使用者名稱*是**nvarchar （128)**，預設值是 NULL。 當這個參數是 NULL 時，Database Mail 不會在這個帳戶上使用驗證。 如果郵件伺服器不需要驗證，使用者名稱便使用 NULL。  
  
 [  **@password**  =] **'***密碼***'**  
 用來登入電子郵件伺服器的密碼。 *密碼*是**nvarchar （128)**，預設值是 NULL。 除非指定了使用者名稱，否則，不需要提供密碼。  
  
 [  **@use_default_credentials**  =] use_default_credentials  
 指定是否要使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的認證將郵件傳送至 SMTP 伺服器。 **use_default_credentials** bit，預設值是 0。 當此參數是 1 時，Database Mail 會使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的認證。 此參數為 0 時，Database Mail 傳送 **@username** 和 **@password** 參數如果有的話，否則會傳送不含 **@username** 和 **@password** 參數。  
  
 [  **@enable_ssl**  =] enable_ssl  
 指定 Database Mail 是否使用安全通訊端層加密通訊。 **Enable_ssl** bit，預設值是 0。  
  
 [  **@account_id**  =] *account_id*輸出  
 傳回新帳戶的帳戶識別碼。 *account_id*是**int**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 Database Mail 提供不同的參數 **@email_address** ，  **@display_name** ，和 **@replyto_address** 。 **@email_address** 參數是傳送訊息的位址。 **@display_name** 參數是顯示的名稱**從：**電子郵件訊息的欄位。 **@replyto_address** 參數是位址將會傳送回覆的電子郵件訊息。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所用的帳戶，可以從只供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用的電子郵件地址傳送電子郵件訊息。 這個地址所送出的訊息應該會顯示易記名稱，使收件者能夠輕鬆判斷是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 送出訊息。 如果收件者回應訊息，這個回應應該會送給資料庫管理員，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所用的地址。 此案例中，此帳戶會使用 **SqlAgent@Adventure-Works.com** 為電子郵件地址。 顯示名稱設定為**SQL Server Agent Automated Mailer**。 此帳戶會使用 **danw@Adventure-Works.com** 當做回應地址，因此回覆給由這個帳戶傳送的郵件移至資料庫管理員，而不是電子郵件地址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式。 Database Mail 分別提供這三個參數的獨立設定，因此，您可以依照需要來設定訊息。  
  
 **@mailserver_type** 參數支援值**'SMTP'**。  
  
 當 **@use_default_credentials** 是 1 時，郵件會傳送到 SMTP 伺服器使用的認證[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 當 **@use_default_credentials** 為 0 和 **@username** 和 **@password** 指定帳戶時，此帳戶會使用 SMTP 驗證。 **@username** 和 **@password** 是此帳戶會使用 SMTP 伺服器，而沒有認證的認證[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或網路上的電腦。  
  
 預存程序**sysmail_add_account_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的帳戶。 這個帳戶所用的電子郵件地址是 `dba@Adventure-Works.com`，它將郵件傳給 SMTP 郵件伺服器 `smtp.Adventure-Works.com`。 電子郵件傳送這個帳戶顯示`AdventureWorks Automated Mailer`上**從：**訊息。 訊息的回應會導向 `danw@Adventure-Works.com`。  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
