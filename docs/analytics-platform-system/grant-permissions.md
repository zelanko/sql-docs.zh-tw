---
title: 授與 T-sql 許可權
description: 針對平行處理資料倉儲中的資料庫作業，授與 T-sql 許可權。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289696"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>授與平行處理資料倉儲的 T-sql 許可權
針對平行處理資料倉儲中的資料庫作業，授與 T-sql 許可權。

## <a name="grant-permissions-to-submit-database-queries"></a>授與提交資料庫查詢的許可權
本節說明如何授與許可權給資料庫角色和使用者，以在 SQL Server PDW 設備上查詢資料。  
  
用來授與查詢資料之許可權的語句取決於所需的存取範圍。 下列 SQL 語句會建立名為 KimAbercrombie 的登入，以存取設備、在**AdventureWorksPDW2012**資料庫中建立名為 KimAbercrombie 的資料庫使用者、建立名為 PDWQueryData 的資料庫角色、將 use KimAbercrombie 新增至 PDWQueryData 角色，然後根據物件或資料庫層級的存取權，顯示授與查詢存取權的選項。  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>授與使用管理主控台的許可權
本節說明如何將許可權授與登入，以使用管理主控台。  
  
**使用管理主控台**  
  
若要使用管理主控台，登入需要伺服器層級**VIEW SERVER STATE**許可權。 下列 SQL 語句會將**VIEW SERVER STATE**許可權授與登`KimAbercrombie`入，讓 Kim 可以使用管理主控台來監視 SQL Server PDW 設備。  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**終止會話**  
  
若要授與登入終止會話的許可權，請授與**ALTER ANY CONNECTION**許可權，如下所示：  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>授與載入資料的許可權
本章節描述如何授與資料庫角色和資料庫使用者的許可權，以將資料載入 SQL Server PDWappliance 上。  
  
下列腳本會顯示每個載入選項所需的許可權。 您可以修改此，以符合您的特定需求。  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>授與從設備資料複製的許可權
本節說明如何授與許可權給使用者或資料庫角色，以從 SQL Server PDW 設備複製資料。  
  
若要將資料移到另一個位置，則需要包含要移動之資料的資料表的**SELECT**許可權。  
  
如果資料的目的地是另一個 SQL Server PDW，則使用者必須擁有目的地的**CREATE TABLE**許可權，以及將包含資料表之架構的**ALTER SCHEMA**許可權。  
  
## <a name="grant-permissions-to-manage-databases"></a>授與管理資料庫的許可權
本節說明如何將許可權授與資料庫使用者，以管理 SQL Server PDW 設備上的資料庫。  
  
在某些情況下，公司會指派資料庫的管理員。 管理員可控制其他登入對資料庫的存取權，以及資料庫中的資料和物件。 若要管理資料庫中的所有物件、角色和使用者，請將資料庫的**CONTROL**許可權授與使用者。 下列語句會將**AdventureWorksPDW2012**資料庫的`KimAbercrombie` **CONTROL**許可權授與使用者。  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
若要授與其他人控制設備上所有資料庫的許可權，請在 master 資料庫中授與**ALTER ANY database**許可權。  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>授與管理登入、使用者和資料庫角色的許可權
本節說明如何授與許可權來管理登入、資料庫使用者和資料庫角色。  
  
### <a name="grant-permissions-to-manage-logins"></a><a name="PermsAdminConsole"></a>授與管理登入的許可權  
**新增或管理登入**  
  
下列 SQL 語句會建立名為 KimAbercrombie 的登入，可以使用[CREATE login](../t-sql/statements/create-login-transact-sql.md)語句來建立新的登入，並使用[alter login](../t-sql/statements/alter-login-transact-sql.md)語句來改變現有的登入。  
  
**ALTER ANY LOGIN**許可權會授與建立新登入和捨棄現有的能力。 一旦登入存在，登入就可以透過具有**ALTER ANY login**許可權或該登入之**alter**許可權的登入來管理。 登入可以變更其本身登入的密碼和預設資料庫。  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>授與管理登入會話的許可權  
若要能夠查看伺服器上的所有會話，需要**VIEW SERVER STATE**許可權。 終止其他登入會話的功能需要**ALTER ANY CONNECTION**許可權。 下列範例會使用稍`KimAbercrombie`早建立的登入。  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>授與管理資料庫使用者的許可權  
建立和卸載資料庫使用者需要**ALTER ANY USER**許可權。 若要管理現有的使用者，則需要該使用者的**ALTER ANY USER**許可權或**alter**許可權。 下列範例會使用稍`KimAbercrombie`早建立的登入。  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>授與許可權以管理資料庫角色  
建立和卸載使用者定義的資料庫角色需要**ALTER ANY ROLE**許可權。 下列範例會使用登`KimAbercrombie`入，並使用稍早建立的。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>登入、使用者和角色許可權圖表  
下列圖表可能會造成混淆，但會顯示較高的杠杆許可權（例如 CONTROL）是否包含可個別授與的更細微許可權（例如 ALTER）。 最佳做法是一律授與最少量的許可權，讓使用者完成必要的工作。 若要這麼做，請授與更明確的許可權，而不是最上層的許可權。  
  
**登入許可權：**  
  
![APS 安全性登入權限](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
使用者權限：****  
  
![APS 安全性使用者權限](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**角色許可權：**  
  
![APS 安全性角色權限](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>授與監視設備的許可權
您可以使用管理主控台或 SQL Server PDW 系統檢視來監視 SQL Server PDW 設備。 登入需要伺服器層級的**VIEW SERVER STATE**許可權，才能監視設備。 登入需要**ALTER ANY CONNECTION**許可權，才能使用管理主控台或**KILL**命令來終止連接。 如需使用管理主控台所需許可權的資訊，請參閱[授與使用管理主控台 &#40;SQL Server PDW&#41;的許可權](#grant-permissions-to-use-the-admin-console)。  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views"></a><a name="PermsAdminConsole"></a>使用系統檢視授與監視設備的許可權  
下列 SQL 語句會建立名為`monitor_login`的登入，並將**VIEW SERVER STATE**許可權`monitor_login`授與此登入。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>使用系統檢視來授與監視設備的許可權，並終止連線  
下列 SQL 語句會建立名`monitor_and_terminate_login`為的登入，並將**VIEW SERVER STATE**和**ALTER ANY CONNECTION**許可權`monitor_and_terminate_login`授與登入。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
若要建立管理員登入，請參閱[固定伺服器角色](pdw-permissions.md#fixed-server-roles)。  
  
## <a name="see-also"></a>另請參閱
[建立登入](../t-sql/statements/create-login-transact-sql.md)  
[建立使用者](../t-sql/statements/create-user-transact-sql.md)  
[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)  
[載入](load-overview.md)  
