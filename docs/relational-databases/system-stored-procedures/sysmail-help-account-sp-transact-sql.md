---
title: sysmail_help_account_sp(轉算-SQL) |微軟文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
author: stevestein
ms.author: sstein
ms.openlocfilehash: ccb5cfd245148c97288a34b1857955f48f3efc73
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528407"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出 Database Mail 帳戶的相關資訊 (密碼除外)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @account_id = ] account_id`要列出其資訊的帳戶 ID。 *account_id* **為 int,** 預設值為 NULL。  
  
`[ @account_name = ] 'account_name'`要為其列出資訊的帳戶的名稱。 *account_name*是**sysname,** 預設值為 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0(** 成功 )或**1(** 失敗 )  
  
## <a name="result-sets"></a>結果集  
 傳回包含下列資料行的結果集。  
  
||||  
|-|-|-|  
|資料行名稱|資料類型|描述|  
|**account_id**|**int**|帳戶的識別碼。|  
|**name**|**sysname**|帳戶的名稱。|  
|**描述**|**nvarchar(256)**|帳戶的描述。|  
|**email_address**|**nvarchar(128)**|傳送訊息的來源電子郵件地址。|  
|**display_name**|**nvarchar(128)**|帳戶的顯示名稱。|  
|**replyto_address**|**nvarchar(128)**|這個帳戶發出的訊息之回應所要送往的地址。|  
|**伺服器類型**|**sysname**|帳戶的電子郵件伺服器類型。|  
|**伺服器名稱**|**sysname**|帳戶的電子郵件伺服器名稱。|  
|**連接埠**|**int**|電子郵件伺服器所用的通訊埠編號。|  
|**使用者**|**nvarchar(128)**|如果電子郵件伺服器使用驗證的話，用來登入電子郵件伺服器的使用者名稱。 當**使用者名**為 NULL 時,資料庫郵件不會為此帳戶使用身份驗證。|  
|**use_default_credentials**|**bit**|指定是否要使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的認證將郵件傳送至 SMTP 伺服器。 **use_default_credentials**位,沒有預設值。 當此參數是 1 時，Database Mail 會使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務的認證。 當此參數為 0 時**\@**,資料庫郵件使用**\@使用者名和密碼**在 SMTP 伺服器上進行身份驗證。 如果**\@使用者名和密碼****\@為**NULL,則資料庫郵件使用匿名身份驗證。 在指定此參數之前，請洽詢 SMTP 管理員。|  
|**enable_ssl**|**bit**|指定資料庫郵件是否使用傳輸層安全 (TLS)加密通訊,以前稱為安全套接字層 (SSL)。 如果您的 SMTP 伺服器上需要 TLS,請使用此選項。 **enable_ssl**位,沒有預設值。 1 指示資料庫郵件使用 TLS 加密通信。 0指示資料庫郵件發送郵件時沒有 TLS 加密。|  
  
## <a name="remarks"></a>備註  
 當未提供*account_id*或*account_name*時 **,sysmail_help_account**列出 Microsoft SQL Server 實例中所有資料庫郵件帳戶的資訊。  
  
 儲存過程**sysmail_help_account_sp**位於**msdb**資料庫中,由**dbo**架構所有。 如果目前資料庫不是**msdb,** 則必須使用三部分名稱執行該過程。  
  
## <a name="permissions"></a>權限  
 將此過程的許可權預設為**sysadmin**固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 **A. 列出所有帳戶的資訊**  
  
 下列範例會顯示如何列出執行個體中之所有帳戶的帳戶資訊。  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 範例結果集如下 (行的長度經過編輯)：  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **B. 列出特定帳戶的資訊**  
  
 下列範例會顯示如何列出名稱為 `AdventureWorks Administrator` 之帳戶的帳戶資訊。  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 範例結果集如下 (行的長度經過編輯)：  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>另請參閱  
 [資料庫郵件](../../relational-databases/database-mail/database-mail.md)   
 [建立資料庫郵件帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [資料庫郵件儲存過程&#40;處理-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
