---
title: EXECUTE AS 子句 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- AS
- AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permission sets [SQL Server]
- queues [SQL Server]
- stored procedures [SQL Server], executing
- user-defined functions [SQL Server], execution context
- EXECUTE AS
- triggers [SQL Server], execution context
- execution context [SQL Server]
- switching execution context
- functions [SQL Server], execution context
ms.assetid: bd517aa3-f06e-4356-87d8-70de5df4494a
caps.latest.revision: 70
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0c2e343bc0272ce2492f8cdba13b2cf5d7eb6162
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="execute-as-clause-transact-sql"></a>EXECUTE AS 子句 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可以定義下列使用者自訂模組的執行內容：函數 (內嵌資料表值函式除外)、程序、佇列和觸發程序。  
  
 您可以指定執行模組的內容，來控制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 是使用哪一個使用者帳戶，以驗證該模組參考之物件的權限。 此舉可以在使用者自訂模組以及其所參考物件之間的物件鏈結管理權限時，提供更大的彈性和控制權。 您只需要授與模組本身的權限給使用者即可，不必授與使用者參考物件的明確權限。 只有執行模組的使用者，必須具有模組所存取之物件的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- SQL Server Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }   
  
DDL Triggers with Server Scope and logon triggers  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'login_name' }   
  
Queues  
{ EXEC | EXECUTE } AS { SELF | OWNER | 'user_name' }   
```  
  
```  
  
-- Windows Azure SQL Database Syntax  
Functions (except inline table-valued functions), Stored Procedures, and DML Triggers  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | OWNER | 'user_name' }   
  
DDL Triggers with Database Scope  
  
{ EXEC | EXECUTE } AS { CALLER | SELF | 'user_name' }  
  
```  
  
## <a name="arguments"></a>引數  
 **CALLER**  
 指定模組內的陳述式，是在該模組的呼叫者內容當中執行。 執行該模組的使用者，不僅必須具有模組本身的適當權限，也必須具有該模組所參考之任何資料庫物件的權限。  
  
 CALLER 是所有模組 (佇列除外) 的預設值，而且與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 行為一樣。  
  
 CALLER 不能在 CREATE QUEUE 或 ALTER QUEUE 陳述式中指定。  
  
 **SELF**  
 EXECUTE AS SELF 相當於 EXECUTE AS *user_name*，其中指定的使用者就是建立或變更模組的人員。 建立或修改模組之人員的實際使用者識別碼，是儲存在 **sys.sql_modules** 或 **sys.service_queues** 目錄檢視的 **execute_as_principal_id** 資料行中。  
  
 SELF 是佇列的預設值。  
  
> [!NOTE]  
>  若要變更 **sys.service_queues** 目錄檢視中 **execute_as_principal_id** 的使用者識別碼，您必須在 ALTER QUEUE 陳述式中明確指定 EXECUTE AS 設定。  
  
 OWNER  
 指定模組內的陳述式，是在該模組目前擁有者的內容中執行。 如果該模組沒有指定的擁有者，則會採用該模組的結構描述擁有者。 DDL 或登入觸發程序不能指定 OWNER。  
  
> [!IMPORTANT]  
>  OWNER 必須對應到單一帳戶，而且不可以是角色或群組。  
  
 **'** *user_name* **'**  
 指定模組內的陳述式，在 *user_name* 指定的使用者內容中執行。 會針對 *user_name* 來驗證模組內任何物件的權限。 *user_name* 無法針對具有伺服器範圍的 DDL 觸發程序或登入觸發程序來指定。 請改為使用 *login_name*。  
  
 *user_name* 必須存在於目前資料庫中，而且必須是單一帳戶。 *user_name* 不可以是群組、角色、憑證、金鑰或內建帳戶，例如 NT AUTHORITY\LocalService、NT AUTHORITY\NetworkService 或 NT AUTHORITY\LocalSystem。  
  
 執行內容的使用者識別碼儲存在中繼資料中，可以在 **sys.sql_modules** 或 **sys.assembly_modules** 目錄檢視的 **execute_as_principal_id** 資料行中檢視。  
  
 **'** *login_name* **'**  
 指定模組內的陳述式，在 *login_name* 所指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入內容中執行。 會針對 *login_name* 來驗證模組內任何物件的權限。 *login_name* 只能針對具有伺服器範圍的 DDL 觸發程序或登入觸發程序來指定。  
  
 *login_name* 不可以是群組、角色、憑證、金鑰或內建帳戶，例如 NT AUTHORITY\LocalService、NT AUTHORITY\NetworkService 或 NT AUTHORITY\LocalSystem。  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 如何評估模組內參考物件的權限，會隨著呼叫物件和所參考物件之間的擁有權鏈結而不同。 在舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，擁有權鏈結是唯一可以避免授與參考物件存取權給呼叫使用者的方法。  
  
 擁有權鏈結具有下列限制：  
  
-   只適用於 DML 陳述式：SELECT、INSERT、UPDATE 和 DELETE。  
  
-   呼叫和被呼叫物件的擁有者必須相同。  
  
-   不適用於模組內的動態查詢。  
  
 無論模組指定的執行內容為何，下列動作一定適用：  
  
-   在執行模組時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會先驗證執行模組的使用者，對該模組具有 EXECUTE 權限。  
  
-   擁有權鏈結規則仍然適用。 換句話說，如果呼叫和被呼叫物件的擁有者一樣，就不會檢查基礎物件的任何權限。  
  
 當使用者執行被指定要在 CALLER 以外之內容執行的模組時，會檢查該使用者執行模組的權限，但是該模組存取物件的其他權限，則是針對 EXECUTE AS 子句中指定的使用者帳戶來執行。 執行該模組的使用者，實際上就是模擬指定的使用者。  
  
 該模組 EXECUTE AS 子句中所指定的內容，只在執行該模組時有效。 模組執行完畢之後，內容便還原給呼叫者。  
  
## <a name="specifying-a-user-or-login-name"></a>指定使用者或登入名稱  
 模組 EXECUTE AS 子句所指定的資料庫使用者或伺服器登入，必須等到修改模組，在其他內容下執行之後，才能夠卸除。  
  
 EXECUTE AS 子句所指定的使用者或登入名稱，必須以主體身分分別存在於 **sys.database_principals** 或 **sys.server_principals** 中，否則建立或變更模組作業就會失敗。 另外，建立或變更模組的使用者，必須具有該主體的 IMPERSONATE 權限。  
  
 如果使用者透過 Windows 群組成員資格，對資料庫或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體具有隱含的存取權，則在 EXECUTE AS 子句中指定的使用者，會在下列一項需求成立，並且在建立好模組時，以隱含方式建立：  
  
-   指定的使用者或登入，是 **sysadmin** 固定伺服器角色的成員。  
  
-   建立該模組的使用者，有權建立主體。  
  
 如果這兩項需求都不符合，則建立模組作業便會失敗。  
  
> [!IMPORTANT]  
>  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 服務是作為本機帳戶 (本機服務或本機使用者帳戶) 使用，就沒有權限可以取得 EXECUTE AS 子句指定之 Windows 網域帳戶的群組成員資格。 此舉會使模組執行作業失敗。  
  
 例如，假設有下列情況：  
  
-   **CompanyDomain\SQLUsers** 群組有權存取 **Sales** 資料庫。  
  
-   **CompanyDomain\SqlUser1** 是 **SQLUsers** 的成員，因此有權存取 **Sales** 資料庫。  
  
-   建立或變更該模組的使用者，有權建立主體。  
  
 在執行下列 `CREATE PROCEDURE` 陳述式時，`CompanyDomain\SqlUser1` 會隱含建立為 `Sales` 資料庫中的資料庫主體。  
  
```  
USE Sales;  
GO  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'CompanyDomain\SqlUser1'  
AS  
SELECT user_name();  
GO  
```  
  
## <a name="using-execute-as-caller-stand-alone-statement"></a>使用 EXECUTE AS CALLER 獨立陳述式  
 請在模組內使用 EXECUTE AS CALLER 獨立陳述式，將執行內容設為模組的呼叫者。  
  
 假設下列預存程序是由 `SqlUser2` 呼叫。  
  
```  
CREATE PROCEDURE dbo.usp_Demo  
WITH EXECUTE AS 'SqlUser1'  
AS  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
EXECUTE AS CALLER;  
SELECT user_name(); -- Shows execution context is set to SqlUser2, the caller of the module.  
REVERT;  
SELECT user_name(); -- Shows execution context is set to SqlUser1.  
GO  
```  
  
## <a name="using-execute-as-to-define-custom-permission-sets"></a>使用 EXECUTE AS 來定義自訂權限集合  
 當您要定義自訂權限集合時，不妨指定模組的執行內容。 例如，有些動作 (例如 TRUNCATE TABLE) 沒有可以授與的權限。 您可以將 TRUNCATE TABLE 陳述式併入模組中，並且指定該模組以有權變更資料表的使用者身分來擴充權限，將資料表在您授與該模組 EXECUTE 權限的使用者處截斷。  
  
 若要以指定的執行內容來檢視模組定義，請使用 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 目錄檢視。  
  
## <a name="best-practice"></a>最佳作法  
 指定一個登入或使用者，它具有執行在模組中定義的作業時所需要的最低權限。 例如，除非需要這些權限，否則不要指定資料庫擁有者帳戶。  
  
## <a name="permissions"></a>Permissions  
 若要執行指定了 EXECUTE AS 的模組，呼叫者必須具有該模組的 EXECUTE 權限。  
  
 若要執行指定了 EXECUTE AS 的 CLR 模組，以存取另一個資料庫或伺服器中的資源，則目標資料庫或伺服器必須信任該模組發源之資料庫 (來源資料庫) 的驗證器。  
  
 若要在建立或修改模組時指定 EXECUTE AS 子句，您必須具有指定之主體的 IMPERSONATE 權限，同時也必須有權建立該模組。 您永遠都可以模擬自己本身。 如果未指定任何執行內容，或者沒有指定 EXECUTE AS CALLER，就不需要 IMPERSONATE 權限。  
  
 若要指定透過 Windows 群組成員資格以具有資料庫之隱含存取權的 *login_name* 或 *user_name*，您必須具有該資料庫的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
 以下範例會在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中建立一個預存程序，並將執行內容指派給 `OWNER`。  
  
```  
CREATE PROCEDURE HumanResources.uspEmployeesInDepartment   
@DeptValue int  
WITH EXECUTE AS OWNER  
AS  
    SET NOCOUNT ON;  
    SELECT e.BusinessEntityID, c.LastName, c.FirstName, e.JobTitle  
    FROM Person.Person AS c   
    INNER JOIN HumanResources.Employee AS e  
        ON c.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN HumanResources.EmployeeDepartmentHistory AS edh  
        ON e.BusinessEntityID = edh.BusinessEntityID  
    WHERE edh.DepartmentID = @DeptValue  
    ORDER BY c.LastName, c.FirstName;  
GO  
  
-- Execute the stored procedure by specifying department 5.  
EXECUTE HumanResources.uspEmployeesInDepartment 5;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.service_queues &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-service-queues-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  
