---
title: sysmail_help_principalprofile_sp (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/02/2016
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
- sysmail_help_principalprofile_sp_TSQL
- sysmail_help_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_principalprofile_sp
ms.assetid: 0cfd6464-09c7-4f03-9d25-58001c096a9e
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd2c499284976a03f601fd43725905d85afd1bdb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailhelpprincipalprofilesp-transact-sql"></a>sysmail_help_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出 Database Mail 設定檔和資料庫主體間之關聯的相關資訊。  
  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_principalprofile_sp [ {   [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ]  
    [ [ , ] {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@principal_id=** ] *principal_id*  
 這是資料庫使用者或角色中的識別碼**msdb**要列出之關聯的資料庫。 *principal_id*是**int**，預設值是 NULL。 任一*principal_id*或*principal_name*可指定。  
  
 [ **@principal_name=** ] **'***principal_name***'**  
 這是資料庫使用者或角色中的名稱**msdb**要列出之關聯的資料庫。 *principal_name*是**sysname**，預設值是 NULL。 任一*principal_id*或*principal_name*可指定。  
  
 [  **@profile_id=** ] *profile_id*  
 這是要列出之關聯的設定檔識別碼。 *profile_id*是**int**，預設值是 NULL。 任一*profile_id*或*profile_name*可指定。  
  
 [  **@profile_name=** ] **'***profile_name***'**  
 這是要列出之關聯的設定檔名稱。 *profile_name*是**sysname**，預設值是 NULL。 任一*profile_id*或*profile_name*可指定。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 傳回包含下表所列資料行的結果集。  
  
||||  
|-|-|-|  
|資料行名稱|資料類型|Description|  
|**principal_id**|**int**|資料庫使用者的識別碼。|  
|**principal_name**|**sysname**|資料庫使用者的名稱。|  
|**profile_id**|**int**|Database Mail 設定檔的識別碼。|  
|**profile_name**|**sysname**|Database Mail 設定檔的名稱。|  
|**is_default**|**bit**|指出設定檔是否為使用者預設設定檔的旗標。|  
  
## <a name="remarks"></a>備註  
 如果**sysmail_help_principalprofile_sp**叫用不含參數，傳回的結果集列出的所有關聯的執行個體中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 否則，結果集會包含符合提供參數之關聯的資訊。 例如，提供設定檔名稱時，程序便會列出設定檔的所有關聯。  
  
 **sysmail_help_principalprofile_sp**處於**msdb**資料庫，擁有者是**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-listing-information-for-a-specific-association"></a>A. 列出特定關聯的資訊  
 下列範例會顯示 `AdventureWorks Administrator` 設定檔和 `ApplicationLogin` 資料庫中的 `msdb` 主體間之所有關聯的資訊。  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp  
    @principal_name = 'danw',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 範例結果集如下 (行的長度經過重新格式化)。  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
5            danw               9           AdventureWorks Administrator   1  
```  
  
### <a name="b-listing-information-for-all-associations"></a>B. 列出所有關聯的資訊  
 下列範例會顯示如何列出執行個體中之所有關聯的資訊。  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp ;  
```  
  
 範例結果集如下 (行的長度經過重新格式化)。  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
6            terrid             3           Product Update Profile         1  
5            danw               9           AdventureWorks Administrator   1  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
