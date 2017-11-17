---
title: "DENY 資料庫權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
- DENY statement, databases
- permissions [SQL Server], databases
- database permissions [SQL Server], denying
- denying permissions [SQL Server], databases
ms.assetid: 36cc4e2c-5a24-4975-9920-9305f12c6e7c
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bddab793d98b4c9ace1fc0af1cda69a81531bf26
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="deny-database-permissions-transact-sql"></a>DENY 資料庫權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  拒絕 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料庫的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DENY <permission> [ ,...n ]    
    TO <database_principal> [ ,...n ] [ CASCADE ]  
    [ AS <database_principal> ]  
  
<permission> ::=    
    permission | ALL [ PRIVILEGES ]  
  
<database_principal> ::=   
    Database_user   
  | Database_role   
  | Application_role   
  | Database_user_mapped_to_Windows_User   
  | Database_user_mapped_to_Windows_Group   
  | Database_user_mapped_to_certificate   
  | Database_user_mapped_to_asymmetric_key   
  | Database_user_with_no_login    
```  
  
## <a name="arguments"></a>引數  
 *權限*  
 指定可以拒絕的資料庫權限。 如需權限清單，請參閱這個主題稍後的「備註」一節。  
  
 ALL  
 這個選項不會拒絕所有可能的權限。 拒絕 ALL 相當於拒絕下列權限：BACKUP DATABASE、BACKUP LOG、CREATE DATABASE、CREATE DEFAULT、CREATE FUNCTION、CREATE PROCEDURE、CREATE RULE、CREATE TABLE 和 CREATE VIEW。  
  
 PRIVILEGES  
 為符合 ISO 而包含這個項目。 不會變更 ALL 的行為。  
  
 CASCADE  
 指出也會對指定主體對其授與權限的主體拒絕權限。  
  
 AS \<database_principal >  
 指定主體，執行這項查詢的主體會從這個主體衍生權限來拒絕權限。  
  
 *Database_user*  
 指定資料庫使用者。  
  
 *Database_role*  
 指定資料庫角色。  
  
 *Application_role*  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定應用程式角色。  
  
 *Database_user_mapped_to_Windows_User*   
  指定對應至 Windows 使用者的資料庫使用者。  
  
 *Database_user_mapped_to_Windows_Group*  
  指定對應至 Windows 群組的資料庫使用者。  
  
 *Database_user_mapped_to_certificate*  
  指定對應至憑證的資料庫使用者。  
  
 *Database_user_mapped_to_asymmetric_key*  
  指定對應至非對稱金鑰的資料庫使用者。  
  
 *Database_user_with_no_login*  
 指定不含對應伺服器層級主體的資料庫使用者。  
  
## <a name="remarks"></a>備註  
 資料庫是由伺服器所包含的安全性實體，而該伺服器是其權限階層中的父系。 下表所列的是可以拒絕之最特定和最有限的資料庫權限，並列出利用隱含方式來併入這些權限的較通用權限。  
  
|資料庫權限|資料庫權限所隱含|伺服器權限所隱含|  
|-------------------------|------------------------------------|----------------------------------|  
|ADMINISTER DATABASE BULK OPERATIONS<br/>**適用於：** [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。|CONTROL|CONTROL SERVER|
|ALTER|CONTROL|ALTER ANY DATABASE|  
|ALTER ANY APPLICATION ROLE|ALTER|CONTROL SERVER|  
|ALTER ANY ASSEMBLY|ALTER|CONTROL SERVER|  
|ALTER ANY ASYMMETRIC KEY|ALTER|CONTROL SERVER|  
|ALTER ANY CERTIFICATE|ALTER|CONTROL SERVER|  
|ALTER ANY COLUMN ENCRYPTION KEY|ALTER|CONTROL SERVER|  
|更改任何資料行主要金鑰定義|ALTER|CONTROL SERVER|  
|ALTER ANY CONTRACT|ALTER|CONTROL SERVER|  
|ALTER ANY DATABASE AUDIT|ALTER|ALTER ANY SERVER AUDIT|  
|ALTER ANY DATABASE DDL TRIGGER|ALTER|CONTROL SERVER|  
|ALTER ANY DATABASE EVENT NOTIFICATION|ALTER|ALTER ANY EVENT NOTIFICATION|  
|ALTER ANY DATABASE EVENT SESSION<br /> **適用於**： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|ALTER|ALTER ANY EVENT SESSION|  
|ALTER ANY DATABASE SCOPED CONFIGURATION<br />  **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。|CONTROL|CONTROL SERVER|  
|ALTER ANY DATASPACE|ALTER|CONTROL SERVER|  
|ALTER ANY EXTERNAL DATA SOURCE|ALTER|CONTROL SERVER|  
|ALTER ANY EXTERNAL FILE FORMAT|ALTER|CONTROL SERVER|  
|改變任何外部程式庫 <br /> **適用於**： [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。|CONTROL|CONTROL SERVER |    
|ALTER ANY FULLTEXT CATALOG|ALTER|CONTROL SERVER|  
|ALTER ANY MASK|CONTROL|CONTROL SERVER|  
|ALTER ANY MESSAGE TYPE|ALTER|CONTROL SERVER|  
|ALTER ANY REMOTE SERVICE BINDING|ALTER|CONTROL SERVER|  
|ALTER ANY ROLE|ALTER|CONTROL SERVER|  
|ALTER ANY ROUTE|ALTER|CONTROL SERVER|  
|ALTER ANY SECURITY POLICY<br /> **適用於**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|CONTROL|CONTROL SERVER|  
|ALTER ANY SCHEMA|ALTER|CONTROL SERVER|  
|ALTER ANY SERVICE|ALTER|CONTROL SERVER|  
|ALTER ANY SYMMETRIC KEY|ALTER|CONTROL SERVER|  
|ALTER ANY USER|ALTER|CONTROL SERVER|  
|AUTHENTICATE|CONTROL|AUTHENTICATE SERVER|  
|BACKUP DATABASE|CONTROL|CONTROL SERVER|  
|BACKUP LOG|CONTROL|CONTROL SERVER|  
|CHECKPOINT|CONTROL|CONTROL SERVER|  
|CONNECT|CONNECT REPLICATION|CONTROL SERVER|  
|CONNECT REPLICATION|CONTROL|CONTROL SERVER|  
|CONTROL|CONTROL|CONTROL SERVER|  
|CREATE AGGREGATE|ALTER|CONTROL SERVER|  
|CREATE ASSEMBLY|ALTER ANY ASSEMBLY|CONTROL SERVER|  
|CREATE ASYMMETRIC KEY|ALTER ANY ASYMMETRIC KEY|CONTROL SERVER|  
|CREATE CERTIFICATE|ALTER ANY CERTIFICATE|CONTROL SERVER|  
|CREATE CONTRACT|ALTER ANY CONTRACT|CONTROL SERVER|  
|CREATE DATABASE|CONTROL|CREATE ANY DATABASE|  
|CREATE DATABASE DDL EVENT NOTIFICATION|ALTER ANY DATABASE EVENT NOTIFICATION|CREATE DDL EVENT NOTIFICATION|  
|CREATE DEFAULT|ALTER|CONTROL SERVER|  
|CREATE FULLTEXT CATALOG|ALTER ANY FULLTEXT CATALOG|CONTROL SERVER|  
|CREATE FUNCTION|ALTER|CONTROL SERVER|  
|CREATE MESSAGE TYPE|ALTER ANY MESSAGE TYPE|CONTROL SERVER|  
|CREATE PROCEDURE|ALTER|CONTROL SERVER|  
|CREATE QUEUE|ALTER|CONTROL SERVER|  
|CREATE REMOTE SERVICE BINDING|ALTER ANY REMOTE SERVICE BINDING|CONTROL SERVER|  
|CREATE ROLE|ALTER ANY ROLE|CONTROL SERVER|  
|CREATE ROUTE|ALTER ANY ROUTE|CONTROL SERVER|  
|CREATE RULE|ALTER|CONTROL SERVER|  
|CREATE SCHEMA|ALTER ANY SCHEMA|CONTROL SERVER|  
|CREATE SERVICE|ALTER ANY SERVICE|CONTROL SERVER|  
|CREATE SYMMETRIC KEY|ALTER ANY SYMMETRIC KEY|CONTROL SERVER|  
|CREATE SYNONYM|ALTER|CONTROL SERVER|  
|CREATE TABLE|ALTER|CONTROL SERVER|  
|CREATE TYPE|ALTER|CONTROL SERVER|  
|CREATE VIEW|ALTER|CONTROL SERVER|  
|CREATE XML SCHEMA COLLECTION|ALTER|CONTROL SERVER|  
|DELETE|CONTROL|CONTROL SERVER|  
|執行 CREATE 陳述式之前，請先執行|CONTROL|CONTROL SERVER|  
|EXECUTE ANY EXTERNAL SCRIPT <br /> **適用於**： [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]。|CONTROL|CONTROL SERVER|   
|INSERT|CONTROL|CONTROL SERVER|  
|KILL DATABASE CONNECTION<br /> **適用於**： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|CONTROL|ALTER ANY CONNECTION|  
|REFERENCES|CONTROL|CONTROL SERVER|  
|SELECT|CONTROL|CONTROL SERVER|  
|SHOWPLAN|CONTROL|ALTER TRACE|  
|SUBSCRIBE QUERY NOTIFICATIONS|CONTROL|CONTROL SERVER|  
|TAKE OWNERSHIP|CONTROL|CONTROL SERVER|  
|UNMASK|CONTROL|CONTROL SERVER|  
|UPDATE|CONTROL|CONTROL SERVER|  
|檢視任何資料行加密金鑰|CONTROL|VIEW ANY DEFINITION|  
|檢視任何主要金鑰定義|CONTROL|VIEW ANY DEFINITION|  
|VIEW DATABASE STATE|CONTROL|VIEW SERVER STATE|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 執行這個陳述式的主體 (或指定了 AS 選項的主體) 必須具有資料庫的 CONTROL 權限，或是具有隱含資料庫 CONTROL 權限的更高權限。  
  
 如果是使用 AS 選項，指定的主體必須擁有資料庫。  
  
## <a name="examples"></a>範例  
  
### <a name="a-denying-permission-to-create-certificates"></a>A. 拒絕建立憑證的權限  
 下列範例會對使用者 `CREATE CERTIFICATE` 拒絕資料庫 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 的 `MelanieK` 權限。  

```  
USE AdventureWorks2012;  
DENY CREATE CERTIFICATE TO MelanieK;  
GO  
```  
  
### <a name="b-denying-references-permission-to-an-application-role"></a>B. 對應用程式角色拒絕 REFERENCES 權限  
 下列範例會對應用程式角色 `REFERENCES` 拒絕資料庫 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 的 `AuditMonitor` 權限。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
```  
USE AdventureWorks2012;  
DENY REFERENCES TO AuditMonitor;  
GO  
```  
  
### <a name="c-denying-view-definition-with-cascade"></a>C. 拒絕具有 CASCADE 的 VIEW DEFINITION  
 下列範例拒絕`VIEW DEFINITION`權限[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]使用者資料庫`CarmineEs`以及所有主體，`CarmineEs`已授與`VIEW DEFINITION`權限。  
  
```  
USE AdventureWorks2012;  
DENY VIEW DEFINITION TO CarmineEs CASCADE;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.database_permissions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [權限 &#40;資料庫引擎&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

