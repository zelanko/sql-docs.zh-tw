---
title: "sysmail_add_profile_sp (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6295b1f239f136c43e00e047186ce408ab9a4a93
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailaddprofilesp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  建立新的 Database Mail 設定檔。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@profile_name** = ] **'***profile_name***'**  
 新設定檔的名稱。 *profile_name*是**sysname**，沒有預設值。  
  
 [ **@description** = ] **'***description***'**  
 新設定檔的選擇性描述。 *描述*是**nvarchar （256)**，沒有預設值。  
  
 [ **@profile_id** = ] *new_profile_id***OUTPUT**  
 傳回新設定檔的識別碼。 *new_profile_id*是**int**，預設值是 NULL。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 Database Mail 設定檔會保存任意數目的 Database Mail 帳戶。 Database Mail 預存程序可以利用這個程序所產生的設定檔名稱或設定檔識別碼來參考設定檔。 如需將帳戶新增至設定檔的詳細資訊，請參閱[sysmail_add_profileaccount_sp &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md).  
  
 預存程序，則可以變更的設定檔名稱和描述**sysmail_update_profile_sp**，而這個設定檔識別碼維持不變的存留期間的設定檔。  
  
 Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的設定檔名稱必須是唯一的，否則，預存程序會傳回一則錯誤。  
  
 預存程序**sysmail_add_profile_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 **A.建立新的設定檔**  
  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的新 Database Mail 設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B.建立新的設定檔，將設定檔識別碼儲存在變數**  
  
 下列範例會建立名稱為 `AdventureWorks Administrator` 的新 Database Mail 設定檔。 這個範例會將設定檔識別碼儲存在 `@profileId` 變數中，且會傳回包含新設定檔之設定檔識別碼的結果集。  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [建立 Database Mail 帳戶](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
