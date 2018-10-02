---
title: REVOKE 可用性群組權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], permissions
- REVOKE statement, availability groups
- revoking permissions, [SQL Server], availability groups
- permissions [SQL Server], availability group
ms.assetid: 02c77378-a36d-4286-9235-d8867a2b92ad
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4be4d925cb90cf02161e71c4797a22e2149b03dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807086"
---
# <a name="revoke-availability-group-permissions-transact-sql"></a>撤銷可用性群組權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  撤銷 AlwaysOn 可用性群組的權限。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON AVAILABILITY GROUP :: availability_group_name  
    { FROM | TO } < server_principal >  [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
        SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey  
```  
  
## <a name="arguments"></a>引數  
 *permission*  
 指定可以撤銷的可用性群組權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 ON AVAILABILITY GROUP **::***availability_group_name*  
 指定要撤銷其權限的可用性群組。 範圍限定詞 (**::**) 是必要項。  
  
 { FROM | TO } \<server_principal> 指定要撤銷其權限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
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
  
> [!IMPORTANT]  
>  獲得授與 WITH GRANT OPTION 之權限的串聯撤銷，會同時撤銷該權限的 GRANT 和 DENY。  
  
 AS *SQL_Server_login*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，執行這項查詢的主體會從這項登入衍生其權限來撤銷權限。  
  
## <a name="remarks"></a>Remarks  
 只有在目前資料庫是 **master** 的情況下，才能夠撤銷伺服器範圍的權限。  
  
 您可以在 [sys.availability_groups & #40;TRANSACT-SQL & #41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) 目錄檢視中，看到有關可用性群組的資訊。 您可以在 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 目錄檢視中，看到伺服器權限的資訊，並在 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 目錄檢視中，看到有關伺服器主體的資訊。  
  
 可用性群組是伺服器層級的安全性實體。 下表所列的是可以撤銷之最特定且最有限的可用性群組權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|可用性群組權限|可用性群組權限所隱含|伺服器權限所隱含|  
|-----------------------------------|----------------------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER ANY AVAILABILITY GROUP|  
|CONNECT|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>[權限]  
 需要可用性群組的 CONTROL 權限或伺服器的 ALTER ANY AVAILABILTIY GROUP 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-revoking-view-definition-permission-on-an-availability-group"></a>A. 撤銷可用性群組的 VIEW DEFINITION 權限  
 下列範例會撤銷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `VIEW DEFINITION` 之可用性群組 `MyAg` 的 `ZArifin` 權限。  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON AVAILABILITY GROUP::MyAg TO ZArifin;  
GO  
```  
  
### <a name="b-revoking-take-ownership-permission-with-the-cascade"></a>B. 撤銷具有 CASCADE 的 TAKE OWNERSHIP 權限  
 下列範例會撤銷 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者 `TAKE OWNERSHIP` 之可用性群組 `MyAg` 的 `PKomosinski` 權限，並從 `PKomosinski` 對其授與 MyAg 之 TAKE OWNERSHIP 的所有主體撤銷該權限。  
  
```  
USE master;  
REVOKE TAKE OWNERSHIP ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    CASCADE;  
GO  
```  
  
### <a name="c-revoking-a-previously-granted-with-grant-option-clause"></a>C. 撤銷先前授與的 WITH GRANT OPTION 子句  
 如果使用 WITH GRANT OPTION 授與權限，則請使用 REVOKE GRANT OPTION FOR … 移除 WITH GRANT OPTION。 下列範例會授與權限，然後移除權限的 WITH GRANT 部分。  
  
```  
USE master;  
GRANT CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski   
    WITH GRANT OPTION;  
GO  
REVOKE GRANT OPTION FOR CONTROL ON AVAILABILITY GROUP::MyAg TO PKomosinski  
CASCADE  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [GRANT 可用性群組權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-availability-group-permissions-transact-sql.md)   
 [DENY 可用性群組權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-availability-group-permissions-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性群組目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

