---
title: "sp_audit_write (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_audit_write
- sp_audit_write_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_audit_write
ms.assetid: 4c523848-1ce6-49ad-92b3-e0e90f24f1c2
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10c74597481f6274485b894c30ac6946bb75fd8a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spauditwrite-transact-sql"></a>sp_audit_write (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將使用者定義稽核事件，以加入**USER_DEFINED_AUDIT_GROUP**。 如果**USER_DEFINED_AUDIT_GROUP**未啟用， **sp_audit_write**會被忽略。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_audit_write [ @user_defined_event_id =  ] user_defined_event_id ,   
        [ @succeeded =  succeeded   
    [ , [ @user_defined_information =  ] 'user_defined_information' ]   
    [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 **@user_defined_event_id**  
 參數使用者所定義，並且記錄在**user_defined_event_id**稽核記錄的資料行。 *@user_defined_event_id*型別**smallint**。  
  
 **@succeeded**  
 由使用者傳遞的參數，指出事件是否成功。 這會顯示在稽核記錄的 succeeded 資料行中。 *@succeeded*是**元**。  
  
 **@user_defined_information**  
 由使用者定義並且記錄在稽核記錄之新 user_defined_event_id 資料行中的文字。 *@user_defined_information*是**nvarchar （4000)**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
 輸入參數錯誤或無法寫入目標稽核記錄都會造成失敗。  
  
## <a name="remarks"></a>備註  
 當**USER_DEFINED_AUDIT_GROUP**加入至伺服器稽核規格或資料庫稽核規格，所觸發的事件**sp_audit_write**將會包含在稽核記錄檔。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**公用**資料庫角色。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-user-defined-audit-event-with-informational-text"></a>A. 建立包含資訊文字的使用者定義稽核事件  
 下列範例會建立識別碼為 27、succeeded 值為 0 而且包含選擇性參考用文字的稽核事件。  
  
```  
EXEC sp_audit_write @user_defined_event_id =  27 ,   
              @succeeded =  0   
            , @user_defined_information = N'Access to a monitored object.' ;  
```  
  
### <a name="b--creating-a-user-defined-audit-event-without-informational-text"></a>B.  建立不包含資訊文字的使用者定義稽核事件  
 下列範例會建立識別碼為 27、succeeded 值為 0 而且不包含選擇性參考用文字或選擇性參數名稱的稽核事件。  
  
```  
EXEC sp_audit_write 27, 0;  
  
```  
  
## <a name="see-also"></a>請參閱  
 [安全性預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
