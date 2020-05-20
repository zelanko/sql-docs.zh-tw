---
title: sysmail_add_principalprofile_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d752015dab48058af18cb981a009691f407da171
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814372"
---
# <a name="sysmail_add_principalprofile_sp-transact-sql"></a>sysmail_add_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授與 msdb 資料庫主體使用 Database Mail 設定檔的許可權。 資料庫主體必須對應至 SQL Server authentication 使用者、Windows 使用者或 Windows 群組。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @principal_id = ] principal_id`關聯之**msdb**資料庫中資料庫使用者或角色的識別碼。 *principal_id*是**int**，預設值是 Null。 必須指定*principal_id*或*principal_name* 。 *Principal_id* **0**會使此設定檔成為公用設定檔，並將存取權授與資料庫中的所有主體。  
  
`[ @principal_name = ] 'principal_name'`關聯的**msdb**資料庫中資料庫使用者或角色的名稱。 *principal_name*是**sysname**，預設值是 Null。 必須指定*principal_id*或*principal_name* 。 「**公用**」 *principal_name*會使此設定檔成為公用設定檔，並將存取權授與資料庫中的所有主體。  
  
`[ @profile_id = ] profile_id`關聯之設定檔的識別碼。 *profile_id*是**int**，預設值是 Null。 必須指定*profile_id*或*profile_name* 。  
  
`[ @profile_name = ] 'profile_name'`關聯的設定檔名稱。 *profile_name*是**sysname**，沒有預設值。 必須指定*profile_id*或*profile_name* 。  
  
`[ @is_default = ] is_default`指定此設定檔是否為主體的預設設定檔。 主體只能有一個預設設定檔。 *is_default*是**bit**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 若要將設定檔設為公用，請指定**0**的** \@ principal_id**或**公用**的** \@ principal_name** 。 **Msdb**資料庫中的所有使用者都可以使用公用設定檔，不過使用者也必須是**DatabaseMailUserRole**的成員，才能執行**sp_send_dbmail**。  
  
 資料庫使用者只能有一個預設設定檔。 當** \@ is_default**為 '**1**'，且使用者已與一或多個設定檔相關聯時，指定的設定檔會成為使用者的預設設定檔。 先前是預設設定檔的設定檔仍會關聯於這位使用者，但已不再是預設設定檔。  
  
 當** \@ is_default**為 '**0**'，而且沒有其他關聯存在時，預存程式會傳回錯誤。  
  
 預存程式**sysmail_add_principalprofile_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱來執行此程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 **A. 建立關聯，設定預設設定檔**  
  
 下列範例會在名為的設定檔 `AdventureWorks Administrator Profile` 與**msdb**資料庫使用者之間建立關聯 `ApplicationUser` 。 設定檔是使用者的預設設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B. 使設定檔成為預設的公用設定檔**  
  
 下列範例會讓設定檔成為 `AdventureWorks Public Profile` **msdb**資料庫中使用者的預設公用設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 設定物件](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
