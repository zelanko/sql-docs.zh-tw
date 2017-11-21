---
title: "還原 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
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
- REVERT_TSQL
- REVERT
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- context switching [SQL Server], reverting
- reverting execution context
- REVERT WITH COOKIE statement
- execution context [SQL Server]
- COOKIE clause
ms.assetid: 4688b17a-dfd1-4f03-8db4-273a401f879f
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 033442da3e10fd834963df30ea071a220464de6f
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="revert-transact-sql"></a>REVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  將執行內容切換回最後一個 EXECUTE AS 陳述式的呼叫端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
REVERT  
    [ WITH COOKIE = @varbinary_variable ]  
```  
  
## <a name="arguments"></a>引數  
 WITH COOKIE = @*varbinary_variable*  
 指定在對應中所建立的 cookie [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)獨立陳述式。 *@varbinary_variable*是**varbinary(100)**。  
  
## <a name="remarks"></a>備註  
 您可以在模組 (例如，預存程序或使用者定義函數，或是獨立陳述式) 中指定 REVERT。 如果 REVERT 是在模組內部指定，則只能用於模組中定義的 EXECUTE AS 陳述式。 例如，下列預存程序會發出後面接有 `EXECUTE AS` 的 `REVERT` 陳述式。  
  
```  
CREATE PROCEDURE dbo.usp_myproc   
  WITH EXECUTE AS CALLER  
AS   
    SELECT SUSER_NAME(), USER_NAME();  
    EXECUTE AS USER = 'guest';  
    SELECT SUSER_NAME(), USER_NAME();  
    REVERT;  
    SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
 假設在預存程序執行的工作階段中，該工作階段的執行內容明確改為 `login1`，如下例所示。  
  
```  
  -- Sets the execution context of the session to 'login1'.  
EXECUTE AS LOGIN = 'login1';  
GO  
EXECUTE dbo.usp_myproc;   
```  
  
 `REVERT`內定義的陳述式`usp_myproc`切換執行內容集模組，但不會影響模組外設定的執行內容。 換句話說，工作階段的執行內容仍然設為 `login1`。  
  
 當 REVERT 被指定為獨立陳述式時，則會套用至批次或工作階段內定義的 EXECUTE AS 陳述式。 如果對應的 EXECUTE AS 陳述式含有 WITH NO REVERT 子句，REVERT 就沒有任何影響。 此時，在工作階段卸除之前，執行內容仍然有效。  
  
## <a name="using-revert-with-cookie"></a>使用 REVERT WITH COOKIE  
 EXECUTE AS 陳述式是用來設定工作階段的執行內容可以包含選擇性子句 WITH NO REVERT COOKIE = @*varbinary_variabl*e。 執行這個陳述式時，[!INCLUDE[ssDE](../../includes/ssde-md.md)]會傳遞 cookie @*varbinary_variabl*e。 執行內容所設定的陳述式只可以還原到先前的內容如果呼叫的 REVERT WITH COOKIE = @*varbinary_variable*陳述式包含正確 *@varbinary_variable* 值。  
  
 這項機制在使用連接共用的環境中相當有用。 連接共用是一組資料庫連接的維護，這些連接是供多位使用者的應用程式重複使用。 因為此值傳遞至 *@varbinary_variable* 只有知道呼叫端的 EXECUTE AS 陳述式 （在此情況下，應用程式），呼叫端可以保證使用者無法變更他們所建立的執行內容會叫用應用程式。 在還原執行內容之後，應用程式就可以將內容切換回另一個主體。  
  
## <a name="permissions"></a>Permissions  
 不需要任何權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-execute-as-and-revert-to-switch-context"></a>A. 使用 EXECUTE AS 及 REVERT 切換內容  
 下列範例會利用多個主體來建立一個內容執行堆疊。 然後再用 REVERT 陳述式，將執行內容重設為前一個呼叫端。 REVERT 陳述式在上移堆疊時會執行多次，直到執行內容設為原始呼叫端為止。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create two temporary principals.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
-- Give IMPERSONATE permissions on user2 to user1  
-- so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
-- Verify that the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
-- Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1, and login2.  
-- The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
-- Remove the temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. 使用 WITH COOKIE 子句  
 下列範例將工作階段的執行內容設定為指定的使用者，並指定 WITH NO REVERT COOKIE = @*varbinary_variabl*e 子句。 `REVERT` 陳述式必須指定傳給 `@cookie` 陳述式中的 `EXECUTE AS` 變數值，才能順利將內容還原回呼叫端。 若要執行這個範例，則必須具備在範例 A 中建立的 `login1` 登入和 `user1` 使用者。  
  
```  
DECLARE @cookie varbinary(100);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie somewhere safe in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(100);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行 AS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EXECUTE AS 子句 &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SUSER_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [USER_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
  

