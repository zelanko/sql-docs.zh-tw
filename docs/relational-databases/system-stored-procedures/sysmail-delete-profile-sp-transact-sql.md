---
title: sysmail_delete_profile_sp (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 601be3bb276576aaaf4c13e42e09d0de41b3b0f7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527980"
---
# <a name="sysmaildeleteprofilesp-transact-sql"></a>sysmail_delete_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  刪除 Database Mail 所用的郵件設定檔。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_profile_sp  { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_id = ] profile_id` 是要刪除的設定檔的設定檔識別碼。 *profile_id*已**int**，預設值是 NULL。 任一*profile_id*或是*profile_name*必須指定。  
  
`[ @profile_name = ] 'profile_name'` 是要刪除的設定檔的名稱。 *profile_name*已**sysname**，預設值是 NULL。 任一*profile_id*或是*profile_name*必須指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 刪除設定檔並不會刪除設定檔所用的帳戶。  
  
 這個預存程序會刪除設定檔，不論使用者是否有權存取設定檔都是如此。 移除使用者的預設私人設定檔或預設公用設定檔時請特別小心**msdb**資料庫。 沒有預設設定檔可用時， **sp_send_dbmail**需要做為引數的設定檔的名稱。 因此，移除預設的設定檔可能會導致呼叫**sp_send_dbmail**失敗。 如需詳細資訊，請參閱 < [sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。  
  
 預存程序**sysmail_delete_profile_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例會刪除名稱為 `AdventureWorks Administrator` 的設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
