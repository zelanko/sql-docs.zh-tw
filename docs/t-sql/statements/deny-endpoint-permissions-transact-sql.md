---
description: DENY 端點權限 (Transact-SQL)
title: DENY 端點權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- endpoints [SQL Server], permissions
- DENY statement, endpoints
- denying permissions [SQL Server], endpoints
- permissions [SQL Server], endpoints
ms.assetid: 3ac40457-7529-4eda-95a4-5247345cc8cf
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9b4af50e021520c1333e0dbffb8cc3c654b6f0fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88416834"
---
# <a name="deny-endpoint-permissions-transact-sql"></a>DENY 端點權限 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  拒絕端點的權限。  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DENY permission  [ ,...n ] ON ENDPOINT :: endpoint_name  
    TO < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *permission*  
 指定可以拒絕的端點權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 ON ENDPOINT **::** _endpoint_name_  
 指定要拒絕其權限的端點。 範圍限定詞 ( **::** ) 是必要項。  
  
 到 \<server_principal>  
 指定要拒絕其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。  
  
 *SQL_Server_login_from_Windows_login*  
 指定從 Windows 登入建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_certificate*  
 指定對應至憑證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_AsymKey*  
 指定對應至非對稱金鑰的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 CASCADE  
 指出目前受到拒絕的權限，也為這個主體曾授與此權限的其他主體所拒絕。  
  
 AS *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，執行這項查詢的主體會從這項登入衍生其權限來拒絕權限。  
  
## <a name="remarks"></a>備註  
 只有在目前資料庫是 **master** 的情況下，才能夠拒絕伺服器範圍的權限。  
  
 您可以在 [sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md) 目錄檢視中，看到有關端點的資訊。 您可以在 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 目錄檢視中，看到伺服器權限的資訊，並在 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 目錄檢視中，看到有關伺服器主體的資訊。  
  
 端點是伺服器層級的安全性實體。 下表所列的是可以拒絕之最特定和最有限的端點權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|端點權限|端點權限所隱含|伺服器權限所隱含|  
|-------------------------|------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY ENDPOINT|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>權限  
 需要端點的 CONTROL 權限或伺服器的 ALTER ANY ENDPOINT 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-denying-view-definition-permission-on-an-endpoint"></a>A. 拒絕端點的 VIEW DEFINITION 權限  
 下列範例拒絕在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 `Mirror7` 端點上，登入 `ZArifin` 的 `VIEW DEFINITION` 權限。  
  
```  
USE master;  
DENY VIEW DEFINITION ON ENDPOINT::Mirror7 TO ZArifin;  
GO  
```  
  
### <a name="b-denying-take-ownership-permission-with-cascade-option"></a>B. 拒絕具有 CASCADE 選項的 TAKE OWNERSHIP 權限  
 下列範例會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者 `TAKE OWNERSHIP` 拒絕端點 `Shipping83` 的 `PKomosinski` 權限，並對 `PKomosinski` 對其授與 `TAKE OWNERSHIP` 的主體拒絕該權限。  
  
```  
USE master;  
DENY TAKE OWNERSHIP ON ENDPOINT::Shipping83 TO PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [GRANT 端點權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [REVOKE 端點權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [端點目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
