---
title: sysmail_add_principalprofile_sp (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
caps.latest.revision: 36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7d5eda99649aa5f27cc199a2a4676c0f79d36c80
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261487"
---
# <a name="sysmailaddprincipalprofilesp-transact-sql"></a>sysmail_add_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授與資料庫使用者或角色使用 Database Mail 設定檔的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@principal_id** = ] *principal_id*  
 資料庫使用者或角色中的識別碼**msdb**之關聯的資料庫。 *principal_id*是**int**，預設值是 NULL。 任一*principal_id*或*principal_name*必須指定。 A *principal_id*的**0** ，這個設定檔的公用設定檔，在資料庫中的所有主體授與存取權。  
  
 [ **@principal_name** = ] **'***principal_name***'**  
 資料庫使用者或角色中的名稱**msdb**之關聯的資料庫。 *principal_name*是**sysname**，預設值是 NULL。 任一*principal_id*或*principal_name*必須指定。 A *principal_name*的 **'public'** ，這個設定檔的公用設定檔，在資料庫中的所有主體授與存取權。  
  
 [ **@profile_id** =] *profile_id*  
 這是關聯的設定檔識別碼。 *profile_id*是**int**，預設值是 NULL。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 這是關聯的設定檔名稱。 *profile_name*是**sysname**，沒有預設值。 任一*profile_id*或*profile_name*必須指定。  
  
 [ **@is_default** = ] *is_default*  
 指定這個設定檔是否為主體的預設設定檔。 主體只能有一個預設設定檔。 *is_default*是**元**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 若要使公用設定檔，指定**@principal_id**的**0**或**@principal_name**的**公用**。 公用設定檔可供所有使用者使用**msdb**資料庫，不過使用者也必須是成員**DatabaseMailUserRole**執行**sp_send_dbmail**。  
  
 資料庫使用者只能有一個預設設定檔。 當**@is_default**是 '**1**' 和使用者在已與一或多個設定檔相關聯，，指定的設定檔會成為使用者的預設設定檔。 先前是預設設定檔的設定檔仍會關聯於這位使用者，但已不再是預設設定檔。  
  
 當**@is_default**是 '**0**' 且沒有任何其他關聯存在，預存程序會傳回錯誤。  
  
 預存程序**sysmail_add_principalprofile_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 **A.建立關聯，設定的預設設定檔**  
  
 下列範例會建立名為設定檔之間的關聯`AdventureWorks Administrator Profile`和**msdb**資料庫使用者`ApplicationUser`。 設定檔是使用者的預設設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B.建立設定檔的預設公用設定檔**  
  
 下列範例會使設定檔`AdventureWorks Public Profile`預設公用設定檔中的使用者**msdb**資料庫。  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 組態物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
