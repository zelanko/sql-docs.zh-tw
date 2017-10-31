---
title: "SET IMPLICIT_TRANSACTIONS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IMPLICIT_TRANSACTIONS
- SET IMPLICIT_TRANSACTIONS
- IMPLICIT_TRANSACTIONS_TSQL
- SET_IMPLICIT_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- implicit transactions
- transactions [SQL Server], implicit
- connections [SQL Server], implicit transaction mode
- SET IMPLICIT_TRANSACTIONS statement
- IMPLICIT_TRANSACTIONS option
ms.assetid: a300ac43-e4c0-4329-8b79-a1a05e63370a
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89211c9b25ea2c488df71456cfbe6a5bc6c48eda
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-implicittransactions-transact-sql"></a>SET IMPLICIT_TRANSACTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  BEGIN TRANSACTION 模式設定為*隱含*，連線。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SET IMPLICIT_TRANSACTIONS { ON | OFF }  
```  
  
## <a name="remarks"></a>備註  
 時，系統是處於*隱含*交易模式。 這表示，如果 @@TRANCOUNT = 0，任何下列的 TRANSACT-SQL 陳述式開始新交易。 相當於看不見的 BEGIN TRANSACTION，以第一次執行：  
  
||||  
|-|-|-|  
|ALTER TABLE|FETCH|REVOKE|  
|BEGIN TRANSACTION|GRANT|SELECT (請參閱底下的例外狀況)。|  
|CREATE|INSERT|TRUNCATE TABLE|  
|DELETE|OPEN|UPDATE|  
|DROP|執行個體時提供 SQL Server 登入。|執行個體時提供 SQL Server 登入。|  
  
 當設為 OFF，每個先前的 T-SQL 陳述式會受限於看不見的 BEGIN TRANSACTION 和 COMMIT TRANSACTION 陳述式看不見。 時，我們稱交易模式是*自動認可*。 如果您的 T-SQL 程式碼會明顯地發出 BEGIN TRANSACTION，我們稱交易模式是*明確*。  
  
 有數個 clarifying 的點，以了解：  
  
-   隱含交易模式時，會發出看不見的 BEGIN TRANSACTION if @@trancount > 已經 0。 不過，任何明確 BEGIN TRANSACTION 陳述式仍會遞增 @@TRANCOUNT。  
  
-   您的 INSERT 陳述式和您的工作單位中的其他任何項目完成時，您必須發出 COMMIT TRANSACTION 陳述式直到 @@TRANCOUNT減量到 0 回。 或者，您可以發出一個 ROLLBACK TRANSACTION。  
  
-   不會從資料表中選取的 SELECT 陳述式將無法開始隱含交易。 例如，`SELECT GETDATE();` 或 `SELECT 1, 'ABC';` 不需要交易。  
  
-   隱含交易意外可能由於 ANSI 預設值是 ON。 如需詳細資訊，請參閱[SET ANSI_DEFAULTS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md).  
  
     IMPLICIT_TRANSACTIONS ON 並不常用。 在大部分情況下，IMPLICIT_TRANSACTIONS 為 ON，這是因為已選擇的 SET ANSI_DEFAULTS ON。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式，自動將 implicit_transactions 設為 OFF 時連接。 SQLClient managed 提供者，使用的連線，並接收透過 HTTP 端點的 SOAP 要求，SET IMPLICIT_TRANSACTIONS 預設值為 OFF。  
  
 若要檢視 IMPLICIT_TRANSACTIONS 的目前設定，請執行下列查詢。  
  
```  
DECLARE @IMPLICIT_TRANSACTIONS VARCHAR(3) = 'OFF';  
IF ( (2 & @@OPTIONS) = 2 ) SET @IMPLICIT_TRANSACTIONS = 'ON';  
SELECT @IMPLICIT_TRANSACTIONS AS IMPLICIT_TRANSACTIONS;  
```  
  
## <a name="examples"></a>範例  
 下列的 TRANSACT-SQL 指令碼會執行幾個不同的測試案例。 也提供文字輸出，其中顯示詳細的行為並從每個測試案例結果。  
  
```tsql  
-- Transact-SQL.  
go  
-- Preparations.  
SET NOCOUNT ON;  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
WHILE (@@TranCount > 0) COMMIT TRANSACTION;  
go  
IF (OBJECT_ID(N'dbo.t1',N'U') IS NOT NULL) DROP TABLE dbo.t1;  
go  
CREATE table dbo.t1 (a int);  
go  
  
PRINT N'-------- [Test A] ---- OFF ----';  
PRINT N'[A.01] Now, SET IMPLICIT_TRANSACTIONS OFF.';  
PRINT N'[A.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
INSERT INTO dbo.t1 VALUES (11);  
INSERT INTO dbo.t1 VALUES (12);  
PRINT N'[A.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test B] ---- ON ----';  
PRINT N'[B.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[B.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
INSERT INTO dbo.t1 VALUES (21);  
INSERT INTO dbo.t1 VALUES (22);  
PRINT N'[B.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[B.04] @@TranCount, after COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test C] ---- ON, then BEGIN TRAN ----';  
PRINT N'[C.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[C.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
BEGIN TRANSACTION;  
INSERT INTO dbo.t1 VALUES (31);  
INSERT INTO dbo.t1 VALUES (32);  
PRINT N'[C.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[C.04] @@TranCount, after a COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
COMMIT TRANSACTION;  
PRINT N'[C.05] @@TranCount, after another COMMIT, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
PRINT N' ';  
PRINT N'-------- [Test D] ---- ON, INSERT, BEGIN TRAN, INSERT ----';  
PRINT N'[D.01] Now, SET IMPLICIT_TRANSACTIONS ON.';  
PRINT N'[D.02] @@TranCount, at start, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
SET IMPLICIT_TRANSACTIONS ON;  
go  
INSERT INTO dbo.t1 VALUES (41);  
BEGIN TRANSACTION;  
INSERT INTO dbo.t1 VALUES (42);  
PRINT N'[D.03] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
COMMIT TRANSACTION;  
PRINT N'[D.04] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
COMMIT TRANSACTION;  
PRINT N'[D.05] @@TranCount, after INSERTs, == ' + CAST(@@TRANCOUNT AS NVARCHAR(10));  
go  
  
-- Clean up.  
SET IMPLICIT_TRANSACTIONS OFF;  
go  
WHILE (@@TranCount > 0) COMMIT TRANSACTION;  
go  
DROP TABLE dbo.t1;  
go  
```  
  
 接下來是前述的 TRANSACT-SQL 指令碼的文字輸出。  
  
```tsql  
-- Text output from Transact-SQL:  
  
-------- [Test A] ---- OFF ----  
[A.01] Now, SET IMPLICIT_TRANSACTIONS OFF.  
[A.02] @@TranCount, at start, == 0  
[A.03] @@TranCount, after INSERTs, == 0  
  
-------- [Test B] ---- ON ----  
[B.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[B.02] @@TranCount, at start, == 0  
[B.03] @@TranCount, after INSERTs, == 1  
[B.04] @@TranCount, after COMMIT, == 0  
  
-------- [Test C] ---- ON, then BEGIN TRAN ----  
[C.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[C.02] @@TranCount, at start, == 0  
[C.03] @@TranCount, after INSERTs, == 2  
[C.04] @@TranCount, after a COMMIT, == 1  
[C.05] @@TranCount, after another COMMIT, == 0  
  
-------- [Test D] ---- ON, INSERT, BEGIN TRAN, INSERT ----  
[D.01] Now, SET IMPLICIT_TRANSACTIONS ON.  
[D.02] @@TranCount, at start, == 0  
[D.03] @@TranCount, after INSERTs, == 2  
[D.04] @@TranCount, after INSERTs, == 1  
[D.05] @@TranCount, after INSERTs, == 0  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [DROP TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [擷取 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [開啟 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/open-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [TRUNCATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

