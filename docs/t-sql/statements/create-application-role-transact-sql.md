---
title: "建立應用程式角色 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APPLICATION_ROLE_TSQL
- CREATE APPLICATION ROLE
- sql13.swb.applicationrole.permissions.f1
- APPLICATION
- APPLICATION ROLE
- CREATE_APPLICATION_ROLE_TSQL
- APPLICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE APPLICATION ROLE statement
- application roles [SQL Server], creating
ms.assetid: 647386da-ee80-41cf-86c9-dd590f9d66b6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 167b3b66439d352cac9632a9b9a2490c1ebaa95b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-application-role-transact-sql"></a>CREATE APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將應用程式角色加入至目前資料庫中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE APPLICATION ROLE application_role_name   
    WITH PASSWORD = 'password' [ , DEFAULT_SCHEMA = schema_name ]  
```  
  
## <a name="arguments"></a>引數  
 *application_role_name*  
 指定應用程式角色的名稱。 這個名稱必須尚未用來參考資料庫中的任何主體。  
  
 密碼**='***密碼***'**  
 指定資料庫使用者要用來啟動應用程式角色的密碼。 您一定要使用增強式密碼。 *密碼*必須符合正在執行的執行個體之電腦的 Windows 密碼原則需求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 DEFAULT_SCHEMA  **=**  *schema_name*  
 指定伺服器在解析這個角色的物件名稱時，將搜尋的第一個結構描述。 如果未定義 DEFAULT_SCHEMA，應用程式角色會將 DBO 用做它的預設結構描述。 *schema_name*可以是不存在於資料庫的結構描述。  
  
## <a name="remarks"></a>備註  
  
> [!IMPORTANT]  
>  設定應用程式角色時會檢查密碼複雜性。 叫用應用程式角色的應用程式必須儲存其密碼。 應用程式角色密碼應該一律以加密方式儲存。  
  
 應用程式角色會顯示在[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)目錄檢視。  
  
 如需如何使用應用程式角色的資訊，請參閱[應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 需要資料庫的 ALTER ANY APPLICATION ROLE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會建立一個稱為 `weekly_receipts` 的應用程式角色，這個應用程式角色將密碼 `987Gbv876sPYY5m23` 和 `Sales` 當做它的預設結構描述。  
  
```  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987G^bv876sPY)Y5m23'   
    , DEFAULT_SCHEMA = Sales;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [應用程式角色](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_setapprole &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [密碼原則](../../relational-databases/security/password-policy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
