---
title: sysmail_add_account_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: stevestein
ms.author: sstein
ms.openlocfilehash: d382d8ee7a871244213467b7a46bdc5b864c55cb
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381897"
---
# <a name="sysmail_add_account_sp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  建立新的 Database Mail 帳戶來保留 SMTP 帳戶的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [transact-sql 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @account_name = ] 'account_name'` 要新增的帳戶名稱。 *account_name*是**sysname**，沒有預設值。  
  
`[ @email_address = ] 'email_address'` 用來傳送訊息的電子郵件地址。 這個地址必須是網際網路電子郵件地址。 *email_address*是**Nvarchar （128）** ，沒有預設值。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式的帳戶可能會從位址**SqlAgent \@Adventure-Works.com**傳送電子郵件。  
  
`[ @display_name = ] 'display_name'` 此帳戶的電子郵件訊息所用的顯示名稱。 *display_name*是**Nvarchar （128）** ，預設值是 Null。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式的帳戶可能會在電子郵件訊息上顯示**SQL Server Agent 自動郵件**的名稱。  
  
`[ @replyto_address = ] 'replyto_address'` 此帳戶的訊息回應傳送至的位址。 *replyto_address*是**Nvarchar （128）** ，預設值是 Null。 例如，回復 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式的帳戶，可能會前往資料庫管理員**danw \@Adventure-Works.com**。  
  
`[ @description = ] 'description'` 是帳戶的描述。 *description*是**Nvarchar （256）** ，預設值是 Null。  
  
`[ @mailserver_name = ] 'server_name'` 要用於此帳戶的 SMTP 郵件伺服器的名稱或 IP 位址。 執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的電腦必須能夠將*server_name*解析為 IP 位址。 *server_name*是**sysname**，沒有預設值。  
  
`[ @mailserver_type = ] 'server_type'` 電子郵件伺服器的類型。 *server_type*是**sysname**，預設值是 **' SMTP '** 。  
  
`[ @port = ] port_number` 電子郵件伺服器的通訊埠編號。 *port_number*是**int**，預設值是25。  
  
`[ @username = ] 'username'` 用來登入電子郵件伺服器的使用者名稱。 使用者*名稱*是**Nvarchar （128）** ，預設值是 Null。 當這個參數是 NULL 時，Database Mail 不會在這個帳戶上使用驗證。 如果郵件伺服器不需要驗證，使用者名稱便使用 NULL。  
  
`[ @password = ] 'password'` 用來登入電子郵件伺服器的密碼。 *password*為**Nvarchar （128）** ，預設值為 Null。 除非指定了使用者名稱，否則，不需要提供密碼。  
  
`[ @use_default_credentials = ] use_default_credentials` 指定是否使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的認證將郵件傳送至 SMTP 伺服器。 **use_default_credentials**是 bit，預設值是0。 當此參數是 1 時，Database Mail 會使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的認證。 當此參數為0時，Database Mail 會傳送 **\@username**和 **\@password**參數（如果有的話），否則會傳送不含 **\@username**和 **\@password**參數的郵件。  
  
`[ @enable_ssl = ] enable_ssl` 指定 Database Mail 是否使用安全通訊端層來加密通訊。 **Enable_ssl**是 bit，預設值是0。  
  
`[ @account_id = ] account_id OUTPUT` 會傳回新帳戶的帳戶識別碼。 *account_id*是**int**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>Remarks  
 Database Mail 提供 **\@email_address**、 **\@display_name**和 **\@replyto_address**的個別參數。 **@No__t_1email_address**參數是傳送訊息的來源位址。 **@No__t_1display_name**參數是電子郵件訊息的 [**寄件者：** ] 欄位中顯示的名稱。 **@No__t_1replyto_address**參數是將傳送電子郵件訊息的位址。 例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所用的帳戶，可以從只供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用的電子郵件地址傳送電子郵件訊息。 這個地址所送出的訊息應該會顯示易記名稱，使收件者能夠輕鬆判斷是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 送出訊息。 如果收件者回應訊息，這個回應應該會送給資料庫管理員，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 所用的地址。 針對此案例，帳戶會使用 **SqlAgent@Adventure-Works.com** 做為電子郵件地址。 [顯示名稱] 設定為 [ **SQL Server Agent 自動郵件**傳送]。 帳戶會使用 **danw@Adventure-Works.com** 做為回復位址，因此，從這個帳戶傳送之訊息的回復，會移至資料庫管理員，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理程式的電子郵件地址。 Database Mail 分別提供這三個參數的獨立設定，因此，您可以依照需要來設定訊息。  
  
 **@No__t_1mailserver_type**參數支援 **' SMTP '** 值。  
  
 當 **\@use_default_credentials**為1時，會使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的認證將郵件傳送至 SMTP 伺服器。 當 **\@use_default_credentials**為0，且已為帳戶指定 **\@username**和 **\@password**時，此帳戶會使用 SMTP 驗證。 **@No__t_1username**和 **\@password**是帳戶用於 SMTP 伺服器的認證，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或電腦所在網路的認證。  
  
 預存程式**sysmail_add_account_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱來執行此程式。  
  
## <a name="permissions"></a>[權限]  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的帳戶。 這個帳戶所用的電子郵件地址是 `dba@Adventure-Works.com`，它將郵件傳給 SMTP 郵件伺服器 `smtp.Adventure-Works.com`。 從這個帳戶傳送的電子郵件訊息會在訊息的 [**寄件者：** ] 行顯示 `AdventureWorks Automated Mailer`。 訊息的回應會導向 `danw@Adventure-Works.com`。  
  
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
 [Database Mail 預存&#40;程式 transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
