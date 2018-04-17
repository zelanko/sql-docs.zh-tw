---
title: sysmail_help_profileaccount_sp (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/09/2016
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
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 652fa8630640233427df040b155ca283b7041d74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailhelpprofileaccountsp-transact-sql"></a>sysmail_help_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出與一個或多個 Database Mail 設定檔相關聯的帳戶。  
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_profileaccount_sp  
   {   [ @profile_id = ] profile_id   
      | [ @profile_name = ] 'profile_name' }  
   [ , {   [ @account_id = ] account_id  
         | [ @account_name = ] 'account_name' } ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@profile_id** =] *profile_id*  
 這是要列出之設定檔的設定檔識別碼。 *profile_id*是**int**，預設值是 NULL。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 這是要列出之設定檔的設定檔名稱。 *profile_name*是**sysname**，預設值是 NULL。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@account_id** = ] *account_id*  
 這是要列出的帳戶識別碼。 *account_id*是**int**，預設值是 NULL。 當*account_id*和*account_name*都是 NULL，會列出設定檔中的所有帳戶。  
  
 [ **@account_name** = ] **'***account_name***'**  
 這是要列出的帳戶名稱。 *account_name*是**sysname**，預設值是 NULL。 當*account_id*和*account_name*都是 NULL，會列出設定檔中的所有帳戶。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 傳回含下列資料行的結果集。  
  
||||  
|-|-|-|  
|資料行名稱|資料類型|Description|  
|**profile_id**|**int**|設定檔的設定檔識別碼。|  
|**profile_name**|**sysname**|設定檔的名稱。|  
|**account_id**|**int**|帳戶的帳戶識別碼。|  
|**account_name**|**sysname**|帳戶的名稱。|  
|**sequence_number**|**int**|帳戶在設定檔內的序號。|  
  
## <a name="remarks"></a>備註  
 若未*profile_id*或*profile_name*指定，此預存程序會傳回執行個體中的每個設定檔的資訊。  
  
 預存程序**sysmail_help_profileaccount_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 **A.依名稱列出特定設定檔的帳戶**  
  
 下列範例會顯示如何指定設定檔名稱來列出 `AdventureWorks Administrator` 設定檔的資訊。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
   @profile_name = 'AdventureWorks Administrator';  
```  
  
 範例結果集如下 (行的長度經過編輯)：  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **B.列出特定的設定檔的設定檔識別碼的帳戶**  
  
 下列範例會顯示如何指定設定檔的設定檔識別碼來列出 `AdventureWorks Administrator` 設定檔的資訊。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
    @profile_id = 131 ;  
```  
  
 範例結果集如下 (行的長度經過編輯)：  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **C.列出所有設定檔的帳戶**  
  
 下列範例會顯示如何列出執行個體中之所有設定檔的帳戶。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp;  
```  
  
 範例結果集如下 (行的長度經過編輯)：  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
106         AdventureWorks Operator      210         Operator-MainServer  1  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
