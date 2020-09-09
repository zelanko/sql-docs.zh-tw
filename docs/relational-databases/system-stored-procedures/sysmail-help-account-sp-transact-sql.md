---
description: sysmail_help_account_sp (Transact-SQL)
title: sysmail_help_account_sp (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 711b0d317b600b455fc4d3d0d80e17e1a9ddf7c3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541040"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  列出 Database Mail 帳戶的相關資訊 (密碼除外)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @account_id = ] account_id` 要列出資訊之帳戶的帳戶識別碼。 *account_id* 是 **int**，預設值是 Null。  
  
`[ @account_name = ] 'account_name'` 要列出資訊的帳戶名稱。 *account_name* 是 **sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
 傳回包含下列資料行的結果集。  
  
| 資料行名稱 | 資料類型 | 描述 |
| ----------- | --------- | ----------- |
|**account_id**|**int**|帳戶的識別碼。|  
|**name**|**sysname**|帳戶的名稱。|  
|**description**|**nvarchar(256)**|帳戶的描述。|  
|**email_address**|**nvarchar(128)**|傳送訊息的來源電子郵件地址。|  
|**display_name**|**nvarchar(128)**|帳戶的顯示名稱。|  
|**replyto_address**|**nvarchar(128)**|這個帳戶發出的訊息之回應所要送往的地址。|  
|**servertype**|**sysname**|帳戶的電子郵件伺服器類型。|  
|**servername**|**sysname**|帳戶的電子郵件伺服器名稱。|  
|**port**|**int**|電子郵件伺服器所用的通訊埠編號。|  
|**username**|**nvarchar(128)**|如果電子郵件伺服器使用驗證的話，用來登入電子郵件伺服器的使用者名稱。 當 **username** 為 Null 時，Database Mail 不會使用此帳戶的驗證。|  
|**use_default_credentials**|**bit**|指定是否要使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的認證將郵件傳送至 SMTP 伺服器。 **use_default_credentials** 是 bit，沒有預設值。 當此參數是 1 時，Database Mail 會使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務的認證。 當這個參數是0時，Database Mail 會使用使用者** \@ 名稱**和** \@ 密碼**在 SMTP 伺服器上進行驗證。 如果使用者** \@ 名稱**和** \@ 密碼**為 Null，則 Database Mail 會使用匿名驗證。 在指定此參數之前，請洽詢 SMTP 管理員。|  
|**enable_ssl**|**bit**|指定 Database Mail 是否使用傳輸層安全性 (TLS) （先前稱為安全通訊端層 (SSL) ）來加密通訊。 如果您的 SMTP 伺服器需要 TLS，請使用此選項。 **enable_ssl** 是 bit，沒有預設值。 1指出 Database Mail 使用 TLS 來加密通訊。 0指出 Database Mail 傳送沒有 TLS 加密的郵件。|  
  
## <a name="remarks"></a>備註  
 未提供 *account_id* 或 *account_name* 時， **sysmail_help_account** 會列出 Microsoft SQL Server 實例中所有 Database Mail 帳戶的資訊。  
  
 預存程式 **sysmail_help_account_sp** 位於 **msdb** 資料庫中，而且是由 **dbo** 架構所擁有。 如果目前的資料庫不是 **msdb**，就必須以三部分名稱執行程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為 **系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
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
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [&#40;Transact-sql&#41;的 Database Mail 預存程式 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
