---
title: sysmail_help_profileaccount_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be5cfcdd06dfeea2215f3c65a2b672b68e28035f
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122687"
---
# <a name="sysmail_help_profileaccount_sp-transact-sql"></a>sysmail_help_profileaccount_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @profile_id = ] profile_id`這是要列出之設定檔的設定檔識別碼。 *profile_id*是**int**，預設值是 Null。 必須指定*profile_id*或*profile_name* 。  
  
`[ @profile_name = ] 'profile_name'`這是要列出之設定檔的設定檔名稱。 *profile_name*是**sysname**，預設值是 Null。 必須指定*profile_id*或*profile_name* 。  
  
`[ @account_id = ] account_id`這是要列出的帳戶識別碼。 *account_id*是**int**，預設值是 Null。 當*account_id*和*ACCOUNT_NAME*都是 Null 時，會列出設定檔中的所有帳戶。  
  
`[ @account_name = ] 'account_name'`這是要列出的帳戶名稱。 *account_name*是**sysname**，預設值是 Null。 當*account_id*和*ACCOUNT_NAME*都是 Null 時，會列出設定檔中的所有帳戶。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 傳回含下列資料行的結果集。  
  
| 資料行名稱 | 資料類型 | 描述 |
| ----------- | --------- | ----------- |
|**profile_id**|**int**|設定檔的設定檔識別碼。|  
|**profile_name**|**sysname**|設定檔的名稱。|  
|**account_id**|**int**|帳戶的帳戶識別碼。|  
|**account_name**|**sysname**|帳戶的名稱。|  
|**sequence_number**|**int**|帳戶在設定檔內的序號。|  
  
## <a name="remarks"></a>備註  
 當未指定*profile_id*或*profile_name*時，這個預存程式會傳回實例中每個設定檔的資訊。  
  
 預存程式**sysmail_help_profileaccount_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱來執行此程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 **A. 依名稱列出特定設定檔的帳戶**  
  
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
  
 **B. 依設定檔識別碼列出特定設定檔的帳戶**  
  
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
  
 **C. 列出所有設定檔帳戶**  
  
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
 [Database Mail 設定物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
