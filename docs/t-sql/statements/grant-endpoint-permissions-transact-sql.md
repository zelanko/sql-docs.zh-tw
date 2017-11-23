---
title: "GRANT 端點權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- endpoints [SQL Server], permissions
- granting permissions [SQL Server], endpoints
- GRANT statement, endpoints
- permissions [SQL Server], endpoints
ms.assetid: 9eda885c-fc3a-4c9d-8de6-ce07fb35a934
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9106f72b1e7d8c137b4a2f80d332db87750309ee
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="grant-endpoint-permissions-transact-sql"></a>GRANT 端點權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授與端點的權限。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
GRANT permission  [ ,...n ] ON ENDPOINT :: endpoint_name  
        TO < server_principal >  [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>引數  
 *權限*  
 指定可以授與的端點權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 端點上**::***endpoint_name*  
 指定要授與其權限的端點。 範圍限定詞 (**::**) 是必要。  
  
 若要\<server_principal >  
 指定要授與其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。  
  
 *SQL_Server_login_from_Windows_login*  
 指定從 Windows 登入建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_certificate*  
 指定對應至憑證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_AsymKey*  
 指定對應至非對稱金鑰的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 WITH GRANT OPTION  
 指出主體也有權授與指定權限給其他主體。  
  
 AS *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，執行這項查詢的主體會從這項登入衍生其權限來授與權限。  
  
## <a name="remarks"></a>備註  
 只有在目前的資料庫時，才可授與伺服器範圍的權限**主要**。  
  
 端點的相關資訊會顯示在[sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)目錄檢視。 伺服器權限的資訊會顯示在[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目錄檢視，以及有關伺服器主體的資訊會顯示在[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目錄檢視。  
  
 端點是伺服器層級的安全性實體。 下表所列的是可以授與之最特定且最有限的端點權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|端點權限|端點權限所隱含|伺服器權限所隱含|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 需要端點的 CONTROL 權限或伺服器的 ALTER ANY ENDPOINT 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-granting-view-definition-permission-on-an-endpoint"></a>A. 授與端點的 VIEW DEFINITION 權限  
 下列範例會將端點 `VIEW DEFINITION` 的 `Mirror7` 權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `ZArifin`。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON ENDPOINT::Mirror7 TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. 授與具有 GRANT OPTION 的 TAKE OWNERSHIP 權限  
 下列範例將端點 `TAKE OWNERSHIP` 的 `Shipping83` 權限授與具有 `PKomosinski` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者 `GRANT OPTION`。  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON ENDPOINT::Shipping83 TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [DENY 端點權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)   
 [REVOKE 端點權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [端點目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [sys.endpoints &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
