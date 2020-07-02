---
title: sysmail_help_profile_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5d98f997c2ab70060aa8770d73c8a8a4823c09bb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752715"
---
# <a name="sysmail_help_profile_sp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  列出一或多個郵件設定檔的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @profile_id = ] profile_id`要傳回信息的設定檔識別碼。 *profile_id*是**int**，預設值是 Null。  
  
`[ @profile_name = ] 'profile_name'`要傳回信息的設定檔名稱。 *profile_name*是**sysname**，預設值是 Null。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 傳回含下列資料行的結果集。  
  
||||  
|-|-|-|  
|資料行名稱|資料類型|描述|  
|**profile_id**|**int**|設定檔的設定檔識別碼。|  
|**name**|**sysname**|設定檔的設定檔名稱。|  
|**description**|**nvarchar(256)**|設定檔的描述。|  
  
## <a name="remarks"></a>備註  
 指定設定檔名稱或設定檔識別碼時， **sysmail_help_profile_sp**會傳回該設定檔的相關資訊。 否則， **sysmail_help_profile_sp**會傳回實例中每個設定檔的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 預存程式**sysmail_help_profile_sp**在**msdb**資料庫中，而且是由**dbo**架構所擁有。 如果目前的資料庫不是**msdb**，就必須以三部分的名稱來執行此程式。  
  
## <a name="permissions"></a>權限  
 此程式的執行許可權預設為**系統管理員（sysadmin** ）固定伺服器角色的成員。  
  
## <a name="examples"></a>範例  
 **A. 列出所有設定檔**  
  
 下列範例會顯示如何列出執行個體中的所有設定檔。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp;  
```  
  
 範例結果集如下 (行的長度經過重新格式化)：  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
57          AdventureWorks Operator       Operator mail profile.          
```  
  
 **B. 列出特定設定檔**  
  
 下列範例會顯示如何列出 `AdventureWorks Administrator` 設定檔的資訊。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 範例結果集如下 (行的長度經過重新格式化)：  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail 預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
