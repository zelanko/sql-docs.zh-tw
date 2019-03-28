---
title: sysmail_delete_principalprofile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae63fabdca36e70daa6da28daa136a5dfcec8e1f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527780"
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除資料庫使用者或使用公用或私人 Database Mail 設定檔之角色的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>引數  
`[ @principal_id = ] principal_id` 是資料庫使用者或角色中的識別碼**msdb**要刪除之關聯的資料庫。 *principal_id*已**int**，預設值是 NULL。 若要讓公用設定檔進入私人設定檔，提供主體識別碼**0**或 主體名稱 **'public'**。 任一*principal_id*或是*principal_name*必須指定。  
  
`[ @principal_name = ] 'principal_name'` 是資料庫使用者或角色的名稱**msdb**要刪除之關聯的資料庫。 *principal_name*已**sysname**，預設值是 NULL。 若要讓公用設定檔進入私人設定檔，提供主體識別碼**0**或 主體名稱 **'public'**。 任一*principal_id*或是*principal_name*必須指定。  
  
`[ @profile_id = ] profile_id` 是要刪除之關聯的設定檔的識別碼。 *profile_id*已**int**，預設值是 NULL。 任一*profile_id*或是*profile_name*必須指定。  
  
`[ @profile_name = ] 'profile_name'` 是要刪除之關聯的設定檔的名稱。 *profile_name*已**sysname**，預設值是 NULL。 任一*profile_id*或是*profile_name*必須指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 若要使公用設定檔進入私人設定檔，提供 **'public'** 主體名稱或**0**主體的識別碼。  
  
 當移除使用者預設私人設定檔的權限，或移除預設公用設定檔的權限時，請特別小心。 沒有預設設定檔可用時， **sp_send_dbmail**需要做為引數的設定檔的名稱。 因此，移除預設的設定檔可能會導致呼叫**sp_send_dbmail**失敗。 如需詳細資訊，請參閱 < [sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。  
  
 預存程序**sysmail_delete_principalprofile_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 下列範例示範刪除設定檔之間的關聯**AdventureWorks Administrator**和 登入**ApplicationUser**中**msdb**資料庫。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
