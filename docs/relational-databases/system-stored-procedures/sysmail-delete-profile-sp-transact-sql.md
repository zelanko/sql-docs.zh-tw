---
title: sysmail_delete_profile_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profile_sp
- sysmail_delete_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profile_sp
ms.assetid: 71998653-4a02-446d-b6f7-50646a29e8a2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 569c2594d060513de99586db64b075be52ed46a9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85639520"
---
# <a name="sysmail_delete_profile_sp-transact-sql"></a>sysmail_delete_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  刪除 Database Mail 所用的郵件設定檔。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_profile_sp  { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_id = ] profile_id`這是要刪除之設定檔的設定檔識別碼。 *profile_id*是**int**，預設值是 Null。 必須指定*profile_id*或*profile_name* 。  
  
`[ @profile_name = ] 'profile_name'`這是要刪除之設定檔的名稱。 *profile_name*是**sysname**，預設值是 Null。 必須指定*profile_id*或*profile_name* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 刪除設定檔並不會刪除設定檔所用的帳戶。  
  
 這個預存程序會刪除設定檔，不論使用者是否有權存取設定檔都是如此。 移除使用者的預設私人設定檔或**msdb**資料庫的預設公用設定檔時，請務必小心。 當沒有可用的預設設定檔時， **sp_send_dbmail**需要設定檔的名稱做為引數。 因此，移除預設設定檔可能會導致**sp_send_dbmail**的呼叫失敗。 如需詳細資訊，請參閱[sp_send_dbmail &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。  
  
 預存程式**sysmail_delete_profile_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱來執行此程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會刪除名稱為 `AdventureWorks Administrator` 的設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 設定物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
