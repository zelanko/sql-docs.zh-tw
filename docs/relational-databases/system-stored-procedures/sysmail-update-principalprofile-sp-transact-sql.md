---
title: sysmail_update_principalprofile_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1bdfeab82f6964abb5e48758cb4b8adba096e5b4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890818"
---
# <a name="sysmail_update_principalprofile_sp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  更新主體與設定檔之間關聯的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>引數  
`[ @principal_id = ] principal_id`要變更之關聯的**msdb**資料庫中，資料庫使用者或角色的識別碼。 *principal_id*是**int**，預設值是 Null。 必須指定*principal_id*或*principal_name* 。  
  
`[ @principal_name = ] 'principal_name'`要更新之關聯的**msdb**資料庫中，資料庫使用者或角色的名稱。 *principal_name*是**sysname**，預設值是 Null。 可以指定*principal_id*或*principal_name* 。  
  
`[ @profile_id = ] profile_id`要變更之關聯的設定檔識別碼。 *profile_id*是**int**，預設值是 Null。 必須指定*profile_id*或*profile_name* 。  
  
`[ @profile_name = ] 'profile_name'`要變更之關聯的設定檔名稱。 *profile_name*是**sysname**，預設值是 Null。 必須指定*profile_id*或*profile_name* 。  
  
`[ @is_default = ] 'is_default'`這是指此設定檔是否為資料庫使用者的預設設定檔。 資料庫使用者只能有一個預設設定檔。 *is_default*是**bit**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 這個預存程序會變更指定的設定檔是否為資料庫使用者之預設設定檔的情況。 資料庫使用者只能有一個預設私人設定檔。  
  
 當關聯的主體名稱為**public** ，或關聯的主體識別碼為**0**時，這個預存程式會變更公用設定檔。 只能有一個預設公用設定檔。  
  
 當** \@ is_default**為 '**1**'，且主體與一個以上的設定檔相關聯時，指定的設定檔會成為主體的預設設定檔。 先前是預設設定檔的設定檔仍會關聯於這個主體，但已不再是預設設定檔。  
  
 預存程式**sysmail_update_principalprofile_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱來執行此程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 **A. 將設定檔設為資料庫的預設公用設定檔**  
  
 下列範例會將設定檔設 `General Use Profile` 為**msdb**資料庫中之使用者的預設公用設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B. 將設定檔設為使用者的預設私人設定檔**  
  
 下列範例會將設定檔設 `AdventureWorks Administrator` 為 `ApplicationUser` **msdb**資料庫中主體的預設設定檔。 這個設定檔必須已關聯於這個主體。 先前是預設設定檔的設定檔仍會關聯於這個主體，但已不再是預設設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 設定物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
