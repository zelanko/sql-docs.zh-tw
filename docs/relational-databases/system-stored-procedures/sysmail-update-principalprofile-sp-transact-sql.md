---
title: sysmail_update_principalprofile_sp (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: fc6e973b71b16817f3e3533544102bfeba3caeb4
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793061"
---
# <a name="sysmailupdateprincipalprofilesp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新主體與設定檔之間關聯的資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>引數  
`[ @principal_id = ] principal_id` 資料庫使用者或角色中的識別碼**msdb**要變更之關聯的資料庫。 *principal_id*已**int**，預設值是 NULL。 任一*principal_id*或是*principal_name*必須指定。  
  
`[ @principal_name = ] 'principal_name'` 資料庫使用者或角色的名稱**msdb**要更新之關聯的資料庫。 *principal_name*已**sysname**，預設值是 NULL。 任一*principal_id*或是*principal_name*可能指定。  
  
`[ @profile_id = ] profile_id` 若要變更關聯的設定檔識別碼。 *profile_id*已**int**，預設值是 NULL。 任一*profile_id*或是*profile_name*必須指定。  
  
`[ @profile_name = ] 'profile_name'` 若要變更關聯的設定檔的名稱。 *profile_name*已**sysname**，預設值是 NULL。 任一*profile_id*或是*profile_name*必須指定。  
  
`[ @is_default = ] 'is_default'` 為此設定檔是否為資料庫使用者的預設設定檔。 資料庫使用者只能有一個預設設定檔。 *is_default*已**元**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 None  
  
## <a name="remarks"></a>備註  
 這個預存程序會變更指定的設定檔是否為資料庫使用者之預設設定檔的情況。 資料庫使用者只能有一個預設私人設定檔。  
  
 關聯的主體名稱時**公開金鑰**關聯的主體識別碼是否**0**，這個預存程序變更公用設定檔。 只能有一個預設公用設定檔。  
  
 當 **\@is_default**是 '**1**' 且主體為多個設定檔相關聯，指定的設定檔會成為主體的預設設定檔。 先前是預設設定檔的設定檔仍會關聯於這個主體，但已不再是預設設定檔。  
  
 預存程序**sysmail_update_principalprofile_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 **A.將設定檔設為資料庫的預設公用設定檔**  
  
 下列範例會將設定檔`General Use Profile`若要在使用者的預設公用設定檔**msdb**資料庫。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B.將設定檔設為使用者的預設私人設定檔**  
  
 下列範例會將設定檔`AdventureWorks Administrator`是主體的預設設定檔`ApplicationUser`中**msdb**資料庫。 這個設定檔必須已關聯於這個主體。 先前是預設設定檔的設定檔仍會關聯於這個主體，但已不再是預設設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
