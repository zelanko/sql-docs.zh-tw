---
title: "授與可用性群組的權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- GRANT statement, availability groups
- granting permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 060eb839-666a-4046-9e1d-5edc9ea75a11
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 154c99ddfb9f3a69a4a9eeae35f20c5e9720100d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="grant-availability-group-permissions-transact-sql"></a>授與可用性群組權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  授與 Alwayson 可用性群組的權限。  
  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
GRANT permission  [ ,...n ] ON AVAILABILITY GROUP :: availability_group_name  
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
 指定可以授與的可用性群組權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 可用性群組上**::***availability_group_name*  
 指定要授與其權限的可用性群組。 範圍限定詞 (**::**) 是必要。  
  
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
  
 可用性群組的相關資訊會顯示在[sys.availability_groups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)目錄檢視。 伺服器權限的資訊會顯示在[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)目錄檢視，以及有關伺服器主體的資訊會顯示在[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)目錄檢視。  
  
 可用性群組是伺服器層級的安全性實體。 下表所列的是可以授與之最特定且最有限的可用性群組權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|可用性群組權限|可用性群組權限所隱含|伺服器權限所隱含|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
 如需的所有圖表[!INCLUDE[ssDE](../../includes/ssde-md.md)]權限，請參閱[Database Engine 的權限海報](http://go.microsoft.com/fwlink/?LinkId=229142)。  
  
## <a name="permissions"></a>Permissions  
 需要可用性群組的 CONTROL 權限或伺服器的 ALTER ANY AVAILABILTIY GROUP 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-granting-view-definition-permission-on-an-availability-group"></a>A. 授與可用性群組的 VIEW DEFINITION 權限  
 下列範例會將可用性群組 `VIEW DEFINITION` 的 `MyAg` 權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `ZArifin`。  
  
```  
USE master;  
GRANT VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-granting-take-ownership-permission-with-the-grant-option"></a>B. 授與具有 GRANT OPTION 的 TAKE OWNERSHIP 權限  
 下列範例會將可用性群組 `TAKE OWNERSHIP` 的 `MyAg` 權限授與具有 `PKomosinski` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者 `GRANT OPTION`。  
  
```  
USE master;  
GRANT TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-control-permission-on-an-availability-group"></a>C. 授與可用性群組的 CONTROL 權限  
 下列範例會將可用性群組 `CONTROL` 的 `MyAg` 權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者 `PKomosinski`。 CONTROL 可完全控制可用性群組的登入，即使不是可用性群組的擁有者亦然。 若要變更擁有權，請參閱[ALTER AUTHORIZATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [撤銷可用性群組的權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revoke-availability-group-permissions-transact-sql.md)   
 [拒絕可用性群組的權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md) [權限 &#40; Database engine&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

