---
title: CREATE SERVER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SERVER_ROLE_TSQL
- CREATE SERVER ROLE
- SERVER ROLE
- CREATE_SERVER_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER ROLE
- SERVER ROLE, CREATE
- CREATE SERVER ROLE statement
- ROLE
- user-defined server roles [SQL Server]
- roles, server
ms.assetid: 30c92f80-f7f6-4a84-ae89-16e69add0de6
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 803c1fccf0369497da75554842d34c72d4c5b95f
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/16/2019
ms.locfileid: "54326809"
---
# <a name="create-server-role-transact-sql"></a>CREATE SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  建立新的使用者定義伺服器角色。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE SERVER ROLE role_name [ AUTHORIZATION server_principal ]  
```  
  
## <a name="arguments"></a>引數  
 *role_name*  
 這是即將建立的伺服器角色名稱。  
  
 AUTHORIZATION *server_principal*  
 這是即將擁有新伺服器角色的登入。 如果未指定任何登入，該伺服器角色便由執行 CREATE SERVER ROLE 的登入所擁有。  
  
## <a name="remarks"></a>Remarks  
 伺服器角色是伺服器層級安全性實體。 當您建立伺服器角色之後，請利用 GRANT、DENY 和 REVOKE，設定角色的伺服器層級權限。 若要將登入新增到伺服器角色，或從其中移除登入，請使用 [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)。 若要卸除伺服器角色，請使用 [DROP SERVER ROLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)。 如需詳細資訊，請參閱 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。  
  
 您可以藉由查詢 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 和 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 目錄檢視，檢視伺服器角色。  
  
 不能將資料庫層級安全性實體授與伺服器角色。 若要建立資料庫角色，請參閱 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)。  
  
 如需設計權限系統的資訊，請參閱 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
## <a name="permissions"></a>[權限]  
 需要 CREATE SERVER ROLE 權限或系統管理員 (sysadmin) 固定伺服器角色中的成員資格。  
  
 此外，也需要登入之 *server_principal* 的 IMPERSONATE、作為 *server_principal*之伺服器角色的 ALTER 權限，或作為 server_principal 之 Windows 群組中的成員資格。  
  
 這會引發 Audit Server Principal Management 事件，且物件類型設定為伺服器角色而事件類型設定為新增。  
  
 當您使用 AUTHORIZATION 選項指派伺服器角色擁有權時，也必須具備下列權限：  
  
-   若要指派伺服器角色擁有權給另一個登入，則需要該登入的 IMPERSONATE 權限。  
  
-   若要指派伺服器角色擁有權給另一個伺服器角色，則需要收件者伺服器角色中的成員資格，或該伺服器角色的 ALTER 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-server-role-that-is-owned-by-a-login"></a>A. 建立登入所擁有的伺服器角色  
 下列範例會建立登入 `buyers` 所擁有的伺服器角色 `BenMiller`。  
  
```  
USE master;  
CREATE SERVER ROLE buyers AUTHORIZATION BenMiller;  
GO  
```  
  
### <a name="b-creating-a-server-role-that-is-owned-by-a-fixed-server-role"></a>B. 建立固定伺服器角色所擁有的伺服器角色  
 下列範例會建立固定伺服器角色 `auditors` 所擁有的伺服器角色 `securityadmin`。  
  
```  
USE master;  
CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [資料庫引擎權限使用者入門](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  
