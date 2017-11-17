---
title: "EXECUTE AS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXECUTE AS
- EXECUTE_AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- WITH NO REVERT clause
- sessions [SQL Server], execution context
- EXECUTE AS
- execution context [SQL Server]
- switching execution context
ms.assetid: 613b8271-7f7d-4378-b7a2-5a7698551dbd
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e389fdc50da662deeab7eba030a367e5fc7e97cb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="execute-as-transact-sql"></a>EXECUTE AS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  設定工作階段的執行內容。  
  
 依預設，工作階段會在使用者登入時起始，在使用者登出時結束。 工作階段期間的所有作業是依對該使用者的權限檢查而定。 當**EXECUTE AS**陳述式執行時，工作階段的執行內容會切換到指定的登入或使用者名稱。 針對該帳戶，而不是呼叫者的登入和使用者安全性權杖內容切換之後，檢查權限**EXECUTE AS**陳述式。 基本上，使用者或登入帳戶的模擬是在工作階段或模組執行的期間，否則會明確還原內容切換。  
  

  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
{ EXEC | EXECUTE } AS <context_specification>  
[;]  
  
<context_specification>::=  
{ LOGIN | USER } = 'name'  
    [ WITH { NO REVERT | COOKIE INTO @varbinary_variable } ]   
| CALLER  
```  
  
## <a name="arguments"></a>引數  
 登入  
 **適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定您要模擬的執行內容是登入。 模擬範圍是在伺服器層級。  
  
> [!NOTE]  
>  無法在自主資料庫或 SQL 資料庫中使用此選項。  
  
 使用者  
 指定您要模擬的內容是目前資料庫中的使用者。 模擬範圍僅限於目前資料庫。 通往資料庫使用者的內容切換不會繼承該使用者的伺服器層級權限。  
  
> [!IMPORTANT]  
>  如果通往資料庫使用者的內容切換在使用中，任何人想要存取資料庫以外的資源，都會導致陳述式失敗。 這包括使用*資料庫*陳述式、 分散式的查詢和查詢會參考使用三或四部分識別碼的另一個資料庫。  
  
 **'** *名稱* **'**  
 有效的使用者或登入名稱。 *名稱*必須是成員**sysadmin**固定伺服器角色，或以主體形式存在於[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)或[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)，分別。  
  
 *名稱*可以指定為本機變數。  
  
 *名稱*必須是單一帳戶，且不能群組、 角色、 憑證、 金鑰或內建帳戶，例如 NT AUTHORITY\LocalService、 NT AUTHORITY\NetworkService 或 NT AUTHORITY\LocalSystem。  
  
 如需詳細資訊，請參閱[指定使用者或登入名稱](#_user)本主題稍後。  
  
 NO REVERT  
 指定內容切換不能還原回先前的內容。 **NO REVERT**選項只能在特定層級。  
  
 如需還原成先前的內容的詳細資訊，請參閱[還原 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revert-transact-sql.md).  
  
 COOKIE 到 **@**  *varbinary_variable*  
 指定執行內容可以只回到先前的內容還原，是否呼叫的 REVERT WITH COOKIE 陳述式包含正確 **@**  *varbinary_variable*值。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]會將 cookie 傳遞 **@**  *varbinary_variable*。 **COOKIE 到**選項只能在特定層級。  
  
 **@***varbinary_variable*是**varbinary （8000)**。  
  
> [!NOTE]  
>  Cookie**輸出**參數目前記載成**varbinary （8000)**這是正確的長度上限。 但目前的實作會傳回**varbinary(100)**。 應用程式應保留**varbinary （8000)** ，讓應用程式能夠繼續正常運作的 cookie 傳回大小如有增加未來的版本。  
  
 CALLER  
 用於模組內部時，指定模組內部的陳述式是在模組呼叫者的內容中執行。  
  
 用於模組外部時，陳述式沒有動作。  
  
## <a name="remarks"></a>備註  
 執行內容中的變更持續有效，直到發生下列項目之一為止：  
  
-   執行另一個 EXECUTE AS 陳述式。  
  
-   執行 REVERT 陳述式。  
  
-   卸除工作階段。  
  
-   造成執行的命令結束的預存程式或觸發程序。  
  
您可以藉由跨多個主體多次呼叫 EXECUTE AS 陳述式來建立執行內容堆疊。 REVERT 陳述式被呼叫時，會將內容切換到內容堆疊中上一層級的登入或使用者。 如需示範此行為，請參閱[範例 A](#_exampleA)。  
  
##  <a name="_user"></a>指定使用者或登入名稱  
 指定在 EXECUTE AS user 或 login 名稱\<context_specification > 必須以主體形式存在於**sys.database_principals**或**sys.server_principals**分別或EXECUTE AS 陳述式會失敗。 此外，還必須授與主體的 IMPERSONATE 權限。 除非呼叫端是資料庫擁有者或隸屬**sysadmin**固定伺服器角色，主體必須存在，即使當使用者存取資料庫或執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]透過 Windows 群組成員資格。 例如，假設有下列情況： 
  
-   **CompanyDomain\SQLUsers**群組具有存取權**銷售**資料庫。  
  
-   **CompanyDomain\SqlUser1**隸屬**SQLUsers** ，因此，具有隱含的存取權**銷售**資料庫。  
  
 雖然**CompanyDomain\SqlUser1**已透過在成員資格資料庫存取**SQLUsers**群組，請在陳述式`EXECUTE AS USER = 'CompanyDomain\SqlUser1'`會失敗，因為`CompanyDomain\SqlUser1`以主體形式不存在資料庫中。  
  
如果使用者被遺棄 （相關登入不存在），而且未建立使用者與**WITHOUT LOGIN**， **EXECUTE AS**的使用者將會失敗。  
  
## <a name="best-practice"></a>最佳作法  
 指定一個登入或使用者，它具有執行工作階段中作業所需要的最低權限。 例如，如果只需要資料庫層級權限，就不要指定具有伺服器層級權限的登入名稱；或者，除非需要其權限，否則不要指定資料庫擁有者帳戶。  
  
> [!CAUTION]  
>  只要 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可以解析名稱，EXECUTE AS 陳述式即可順利地運作。 即使 Windows 使用者無權存取 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，只要網域使用者存在，Windows 或許可以解析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的使用者。 這可能會導致無權存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的使用者順利地登入，但模擬登入只有 public 或 guest 的權限。  
  
## <a name="using-with-no-revert"></a>使用 WITH NO REVERT  
 當 EXECUTE AS 陳述式包括選擇性的 WITH NO REVERT 子句時，不能使用 REVERT 或藉由執行另一個 EXECUTE AS 陳述式來重設工作階段的執行內容。 陳述式設定的內容會持續有效，直到卸除工作階段為止。  
  
 當 WITH NO REVERT COOKIE = @*varbinary_variabl*指定 e 子句時，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]會將 cookie 傳遞到 @*varbinary_variabl*e。 執行內容所設定的陳述式只可以還原到先前的內容如果呼叫的 REVERT WITH COOKIE = @*varbinary_variable*陳述式包含相同 *@varbinary_variable* 值。  
  
 這個選項在使用連接共用的環境中相當有用。 連接共用是資料庫連接群組的維護，這些連接是供應用程式伺服器上的應用程式重複使用。 因為此值傳遞至 *@varbinary_variable* 只有知道呼叫端的 EXECUTE AS 陳述式，呼叫端可以保證它們建立的執行內容，無法變更其他人。  
  
## <a name="determining-the-original-login"></a>決定原始登入  
 使用[ORIGINAL_LOGIN](../../t-sql/functions/original-login-transact-sql.md)函數來傳回連接到的執行個體的登入名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以利用這個函數來傳回有許多明確或隱含內容切換的工作階段中原始登入的識別。  
  
## <a name="permissions"></a>Permissions  
 若要指定**EXECUTE AS**登入，呼叫端必須具有**IMPERSONATE**指定登入權限名稱，並不應遭到拒絕**IMPERSONATE ANY LOGIN**權限. 若要指定**EXECUTE AS**呼叫端必須具有資料庫使用者， **IMPERSONATE**權限指定的使用者名稱。 當**EXECUTE AS CALLER**指定，則**IMPERSONATE**沒有必要權限。  
  
## <a name="examples"></a>範例  
  
###  <a name="_exampleA"></a> A. 使用 EXECUTE AS 及 REVERT 切換內容  
 下列範例會利用多個主體來建立一個內容執行堆疊。 然後再用 `REVERT` 陳述式，將執行內容重設為前一個呼叫者。 `REVERT` 陳述式在上移堆疊時會執行多次，直到執行內容設為原始呼叫者為止。  
  
```  
USE AdventureWorks2012;  
GO  
--Create two temporary principals  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
--Give IMPERSONATE permissions on user2 to user1  
--so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
--Verify the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
--Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1 and login2.  
--The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
--Remove temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. 使用 WITH COOKIE 子句  
 下列範例將工作階段的執行內容設定為指定的使用者，並指定 WITH NO REVERT COOKIE = @*varbinary_variabl*e 子句。 `REVERT` 陳述式必須指定傳給 `@cookie` 陳述式中的 `EXECUTE AS` 變數值，才能順利將內容還原回呼叫端。 若要執行這個範例，則必須具備在範例 A 中建立的 `login1` 登入和 `user1` 使用者。  
  
```  
DECLARE @cookie varbinary(8000);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie in a safe location in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(8000);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [還原 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)  
  
  


