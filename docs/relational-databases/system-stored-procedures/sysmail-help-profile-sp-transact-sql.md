---
title: sysmail_help_profile_sp (TRANSACT-SQL) |Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b953f619ab422eba81a925375d9ae8b0cd60e82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836456"
---
# <a name="sysmailhelpprofilesp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出一或多個郵件設定檔的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@profile_id** =] *profile_id*  
 要傳回資訊的設定檔識別碼。 *profile_id*已**int**，預設值是 NULL。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 要傳回資訊的設定檔名稱。 *profile_name*已**sysname**，預設值是 NULL。  
  
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
 當指定的設定檔名稱或設定檔識別碼時， **sysmail_help_profile_sp**傳回該設定檔的相關資訊。 否則，請**sysmail_help_profile_sp**會傳回每個設定檔中的資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。  
  
 預存程序**sysmail_help_profile_sp**處於**msdb**資料庫中，擁有者**dbo**結構描述。 此程序必須利用三部分名稱來執行，如果目前的資料庫不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 執行此程序預設值，成員的權限**sysadmin**固定的伺服器角色。  
  
## <a name="examples"></a>範例  
 **A.列出所有設定檔**  
  
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
  
 **B.列出特定設定檔**  
  
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
 [Database Mail 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
