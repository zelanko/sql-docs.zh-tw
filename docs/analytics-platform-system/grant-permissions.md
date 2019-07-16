---
title: 授與 T-SQL 權限-Parallel Data Warehouse |Microsoft Docs
description: 授與 T-SQL 平行處理資料倉儲的資料庫作業的權限。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 15798edc4d6a9b1f00c8dd489dfed76a39e5f340
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960940"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>授與 T-SQL 平行處理資料倉儲的權限
授與 T-SQL 平行處理資料倉儲的資料庫作業的權限。

## <a name="grant-permissions-to-submit-database-queries"></a>提交資料庫查詢的權限授與
本節說明如何授與權限給資料庫角色和 SQL Server PDW 應用裝置上的查詢資料的使用者。  
  
用來授與權限來查詢資料的陳述式會取決於所需的存取範圍。 下列 SQL 陳述式建立名為 KimAbercrombie，可存取設備，建立名為 KimAbercrombie 中的資料庫使用者的登入**AdventureWorksPDW2012**資料庫，建立名為 PDWQueryData 的資料庫角色，新增使用 KimAbercrombie 至 PDWQueryData 角色，然後顯示選項，來授與查詢權限，根據是否在物件或資料庫層級授與存取權。  
  
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
  
## <a name="grant-permissions-to-use-the-admin-console"></a>若要使用系統管理員主控台的權限授與
本節說明如何授與權限給登入，使用系統管理主控台。  
  
**使用系統管理主控台**  
  
若要使用管理主控台登入需要伺服器層級**VIEW SERVER STATE**權限。 下列 SQL 陳述式會授與**VIEW SERVER STATE**登入的權限`KimAbercrombie`以便 Kim 可以使用管理主控台來監視 SQL Server PDW 應用裝置。  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**終止工作階段**  
  
若要授與登入終止工作階段的權限，授與**ALTER ANY CONNECTION**權限，如下所示：  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>若要載入資料的權限授與
本節說明如何授與權限給資料庫角色和資料庫使用者，將 SQL Server PDWappliance 的資料載入。  
  
下列指令碼所示的權限所需的每一個載入選項。 您可以修改此選項以符合您特定需求。  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>授與權限，將資料複製在應用裝置外。
本節說明如何授與權限的使用者或資料庫角色將在 SQL Server PDW 應用裝置外的資料複製。  
  
若要將資料移至另一個位置，需要**選取**包含資料的資料表的權限，才能移動。  
  
如果另一個 SQL Server PDW 資料的目的地，使用者必須具有**CREATE TABLE**目的地的權限並**ALTER SCHEMA**將包含資料表的結構描述權限。  
  
## <a name="grant-permissions-to-manage-databases"></a>授與權限來管理資料庫
本節說明如何將權限授與資料庫使用者來管理 SQL Server PDW 應用裝置上的資料庫。  
  
在某些情況下，某家公司會指派資料庫的管理員。 管理員控制的其他登入擁有資料庫，以及資料和資料庫中的物件的存取權。 若要管理所有物件，角色，並在資料庫中的使用者授與使用者**控制**資料庫的權限。 下列陳述式會授與**控制**權限**AdventureWorksPDW2012**給使用者的資料庫`KimAbercrombie`。  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
若要授與其他人來控制應用裝置上的所有資料庫的權限，授與**ALTER ANY DATABASE** master 資料庫中的權限。  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>管理登入、 使用者和資料庫角色的權限授與
本節說明如何授與權限來管理登入、 資料庫使用者和資料庫角色。  
  
### <a name="PermsAdminConsole"></a>若要管理的登入授與權限  
**新增或管理登入**  
  
下列 SQL 陳述式建立名為 KimAbercrombie 可以藉由建立新的登入的登入[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)陳述式並使用修改現有的登入[ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)陳述式。  
  
**ALTER ANY LOGIN**權限授與建立新的登入和卸除現有的能力。 具有登入之後的登入存在，可以管理登入**ALTER ANY LOGIN**權限或**ALTER**該登入權限。 登入可以變更自己的登入的密碼和預設資料庫。  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>授與權限來管理登入工作階段  
若要能夠在伺服器上檢視所有工作階段，需要**VIEW SERVER STATE**權限。 需要能夠終止工作階段內的其他登入**ALTER ANY CONNECTION**權限。 下列範例會使用`KimAbercrombie`稍早建立的登入。  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>管理資料庫使用者的權限授與  
建立和卸除資料庫使用者需要**ALTER ANY USER**權限。 管理現有的使用者需要**ALTER ANY USER**權限或**ALTER**對該使用者的權限。 下列範例會使用`KimAbercrombie`稍早建立的登入。  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>授與管理資料庫角色的權限  
建立和卸除使用者定義資料庫角色需要**ALTER ANY ROLE**權限。 下列範例會使用`KimAbercrombie`登入和稍早建立的使用。  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>登入、 使用者和角色的權限圖表  
下列圖表可能會造成混淆，但它們會示範如何更高等級權限 （例如控制項） 包含更細微的權限可以授與個別 （例如 ALTER)。 最好一律授與最少的人完成其必要工作的權限。 若要這樣做，請授與更特定的權限，而不是最高層級權限。  
  
**登入權限：**  
  
![APS 安全性登入權限](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**使用者的權限：**  
  
![APS 安全性使用者權限](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**角色權限：**  
  
![APS 安全性角色權限](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>授與權限，來監視設備
使用 系統管理員主控台 或 SQL Server PDW 系統檢視表，可以監視 SQL Server PDW 應用裝置。 登入需要伺服器層級**VIEW SERVER STATE**監視設備的權限。 登入時，需要**ALTER ANY CONNECTION**終止連線，使用系統管理員主控台的權限或**KILL**命令。 如需使用管理主控台所需的權限資訊，請參閱[授與權限，才能使用系統管理員主控台&#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console)。  
  
### <a name="PermsAdminConsole"></a>授與權限來使用系統檢視來監視設備  
下列 SQL 陳述式建立名為登入`monitor_login`，並授與**VIEW SERVER STATE**權限`monitor_login`登入。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>授與權限來使用系統檢視來監視設備，以及終止連線  
下列 SQL 陳述式建立名為登入`monitor_and_terminate_login`，並授與**VIEW SERVER STATE**並**ALTER ANY CONNECTION**權限`monitor_and_terminate_login`登入。  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
若要建立系統管理員登入，請參閱[固定伺服器角色](pdw-permissions.md#fixed-server-roles)。  
  
## <a name="see-also"></a>另請參閱
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[建立使用者](../t-sql/statements/create-user-transact-sql.md)  
[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)  
[載入](load-overview.md)  
