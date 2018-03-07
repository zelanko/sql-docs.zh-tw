---
title: "REVOKE 端點權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- endpoints [SQL Server], permissions
- REVOKE statement, endpoints
- permissions [SQL Server], endpoints
ms.assetid: 826f513e-9ad0-46b9-87ad-7525713638c8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a02fa4d0d19e52599b8b148410e099f989afe4f3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="revoke-endpoint-permissions-transact-sql"></a>REVOKE 端點權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤銷授與或拒絕的端點權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON ENDPOINT :: endpoint_name  
    { FROM | TO } <server_principal> [ ,...n ]  
    [ CASCADE ]  
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
  
 {從 |為} \<server_principal > 指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在撤銷權限的登入。  
  
 *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的名稱。  
  
 *SQL_Server_login_from_Windows_login*  
 指定從 Windows 登入建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_certificate*  
 指定對應至憑證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 *SQL_Server_login_from_AsymKey*  
 指定對應至非對稱金鑰的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。  
  
 GRANT OPTION  
 指出會撤銷對其他主體授與指定權限的權限。 不會撤銷權限本身。  
  
> [!IMPORTANT]  
>  如果主體有不含 GRANT 選項的指定權限，則會撤銷權限本身。  
  
 CASCADE  
 指出目前正在撤銷的權限，而這個權限也會被這個主體所授與或拒絕的其他主體所撤銷。  
  
> [!CAUTION]  
>  獲得授與 WITH GRANT OPTION 之權限的串聯撤銷，會同時撤銷該權限的 GRANT 和 DENY。  
  
 AS *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，執行這項查詢的主體會從這項登入衍生其權限來撤銷權限。  
  
## <a name="remarks"></a>備註  
 只有當目前資料庫是可以撤銷伺服器範圍的權限**主要**。  
  
 端點的相關資訊會顯示在[sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)目錄檢視。 伺服器權限的資訊會顯示在[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目錄檢視，以及有關伺服器主體的資訊會顯示在[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目錄檢視。  
  
 端點是伺服器層級的安全性實體。 下表所列的是可以撤銷之最特定且最有限的端點權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
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
  
### <a name="a-revoking-view-definition-permission-on-an-endpoint"></a>A. 撤銷端點的 VIEW DEFINITION 權限  
 下列範例會撤銷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `VIEW DEFINITION` 之端點 `Mirror7` 的 `ZArifin` 權限。  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON ENDPOINT::Mirror7 FROM ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade-option"></a>B. 撤銷具有 CASCADE 選項的 TAKE OWNERSHIP 權限  
 下列範例會撤銷`TAKE OWNERSHIP`端點的權限`Shipping83`從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者`PKomosinski`往來的所有主體`PKomosinski`授與`TAKE OWNERSHIP`上`Shipping83`。  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON ENDPOINT::Shipping83 FROM PKomosinski   
    CASCADE;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [GRANT 端點權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [DENY 端點權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/deny-endpoint-permissions-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [端點目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [sys.endpoints &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

