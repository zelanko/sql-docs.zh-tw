---
title: "SET CURSOR_CLOSE_ON_COMMIT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CURSOR_CLOSE_ON_COMMIT
- SET CURSOR_CLOSE_ON_COMMIT
- CURSOR_CLOSE_ON_COMMIT_TSQL
- SET_CURSOR_CLOSE_ON_COMMIT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- CURSOR_CLOSE_ON_COMMIT option
- transactions [SQL Server], cursors
- closing cursors
- cursors [SQL Server], closing
- SET CURSOR_CLOSE_ON_COMMIT statement
ms.assetid: 7b976154-98ce-4a06-bbae-7e59c34211f7
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49e829a63d87485a2834094327195cffcec9a53c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="set-cursorcloseoncommit-transact-sql"></a>SET CURSOR_CLOSE_ON_COMMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  控制 [!INCLUDE[tsql](../../includes/tsql-md.md)] COMMIT TRANSACTION 陳述式的行為。 這項設定的預設值是 OFF。 這表示當您認可交易時，伺服器不會關閉資料指標。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET CURSOR_CLOSE_ON_COMMIT { ON | OFF }  
```  
  
## <a name="remarks"></a>備註  
 當 SET CURSOR_CLOSE_ON_COMMIT 為 ON 時，這項設定會遵照 ISO 標準，在認可或回復時關閉任何開啟的資料指標。 當 SET CURSOR_CLOSE_ON_COMMIT 為 OFF 時，在認可交易時，不會關閉資料指標。  
  
> [!NOTE]  
>  如果 SET CURSOR_CLOSE_ON_COMMIT 是 ON，當從 SAVE TRANSACTION 陳述式中將回復套用在 savepoint_name 上，在回復時，並不會關閉開啟的資料指標。  
  
 如果 SET CURSOR_CLOSE_ON_COMMIT 是 OFF，ROLLBACK 陳述式只會關閉開啟而尚未完全擴展的非同步資料指標。 如果回復修改的話，在修改之後開啟的 STATIC 或非感應式資料指標將不再反映資料的狀態。  
  
 SET CURSOR_CLOSE_ON_COMMIT 會控制 CURSOR_CLOSE_ON_COMMIT 資料庫選項的相同行為。 如果 CURSOR_CLOSE_ON_COMMIT 設為 ON 或 OFF，便會在連接上使用這項設定。 如果未指定 SET CURSOR_CLOSE_ON_COMMIT 中的值**sys.databases**中的資料行**sys.databases**目錄檢視會套用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驅動程式同時設定 CURSOR_CLOSE_ON_COMMIT 為 OFF 連線時。 DB-Library 不會自動設定 CURSOR_CLOSE_ON_COMMIT 值。  
  
 當 SET ANSI_DEFAULTS 是 ON 時，會啟用 SET CURSOR_CLOSE_ON_COMMIT。  
  
 SET CURSOR_CLOSE_ON_COMMIT 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 若要檢視此設定的目前設定，請執行下列查詢。  
  
```  
DECLARE @CURSOR_CLOSE VARCHAR(3) = 'OFF';  
IF ( (4 & @@OPTIONS) = 4 ) SET @CURSOR_CLOSE = 'ON';  
SELECT @CURSOR_CLOSE AS CURSOR_CLOSE_ON_COMMIT;  
```  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例定義交易中的資料指標，且在交易認可之後，會嘗試使用它。  
  
```  
-- SET CURSOR_CLOSE_ON_COMMIT  
-------------------------------------------------------------------------------  
SET NOCOUNT ON;  
  
CREATE TABLE t1 (a INT);  
GO   
  
INSERT INTO t1   
VALUES (1), (2);  
GO  
  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT ON';  
GO  
SET CURSOR_CLOSE_ON_COMMIT ON;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
PRINT '-- SET CURSOR_CLOSE_ON_COMMIT OFF';  
GO  
SET CURSOR_CLOSE_ON_COMMIT OFF;  
GO  
PRINT '-- BEGIN TRAN';  
BEGIN TRAN;  
PRINT '-- Declare and open cursor';  
DECLARE testcursor CURSOR FOR  
    SELECT a FROM t1;  
OPEN testcursor;  
PRINT '-- Commit tran';  
COMMIT TRAN;  
PRINT '-- Try to use cursor';  
FETCH NEXT FROM testcursor;  
CLOSE testcursor;  
DEALLOCATE testcursor;  
GO  
DROP TABLE t1;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [關閉 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)  
  
  
