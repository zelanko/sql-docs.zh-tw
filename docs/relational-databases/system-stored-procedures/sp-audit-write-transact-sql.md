---
title: sp_audit_write （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_audit_write
- sp_audit_write_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_audit_write
ms.assetid: 4c523848-1ce6-49ad-92b3-e0e90f24f1c2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 371bbb36abd6362c9724604a102f590869a74cc2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716168"
---
# <a name="sp_audit_write-transact-sql"></a>sp_audit_write (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將使用者定義的 audit 事件加入至**USER_DEFINED_AUDIT_GROUP**。 如果未啟用**USER_DEFINED_AUDIT_GROUP** ， **sp_audit_write**會被忽略。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_audit_write [ @user_defined_event_id = ] user_defined_event_id
    [ , [ @succeeded = ] succeeded ]
    [ , [ @user_defined_information = ] 'user_defined_information' ]
    [ ; ]
```  
  
## <a name="arguments"></a>引數  
 `[ @user_defined_event_id = ] user_defined_event_id`  
 使用者定義的參數，並記錄在 audit 記錄檔的**user_defined_event_id**資料行中。 * \@ user_defined_event_id*的類型為**Smallint**。  
  
 `[ @succeeded = ] succeeded`  
 由使用者傳遞的參數，指出事件是否成功。 這會顯示在稽核記錄的 succeeded 資料行中。 `@succeeded`是**bit**。  
  
 `[ @user_defined_information = ] 'user_defined_information'`  
 由使用者定義並且記錄在稽核記錄之新 user_defined_event_id 資料行中的文字。 `@user_defined_information`是**Nvarchar （4000）**。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
 輸入參數錯誤或無法寫入目標稽核記錄都會造成失敗。  
  
## <a name="remarks"></a>備註  
 當**USER_DEFINED_AUDIT_GROUP**新增至伺服器 audit 規格或資料庫審核規格時， **sp_audit_write**所觸發的事件就會包含在 AUDIT 記錄中。  
  
## <a name="permissions"></a>權限  
 需要**public**資料庫角色中的成員資格。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的安全性預存程式](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [server_principals &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
