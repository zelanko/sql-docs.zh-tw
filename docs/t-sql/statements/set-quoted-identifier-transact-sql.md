---
title: "SET QUOTED_IDENTIFIER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 02/03/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUOTED_IDENTIFIER_TSQL
- SET_QUOTED_IDENTIFIER_TSQL
- SET QUOTED_IDENTIFIER
- QUOTED_IDENTIFIER
dev_langs: TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- identifiers [SQL Server], delimited
- QUOTED_IDENTIFIER option
- quoted identifiers
- ISO delimited identifiers rules
- SET QUOTED_IDENTIFIER statement
ms.assetid: 10f66b71-9241-4a3a-9292-455ae7252565
caps.latest.revision: "48"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 207cf23523a315a0a4a4bc923ae9e52d7b82f8b0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="set-quotedidentifier-transact-sql"></a>SET QUOTED_IDENTIFIER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 遵照有關分隔識別碼和常值字串之引號的 ISO 規則。 用雙引號定界的識別碼可以是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 保留關鍵字，也可以包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的識別碼語法規則通常不接受的字元。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET QUOTED_IDENTIFIER { ON | OFF }  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET QUOTED_IDENTIFIER ON   
```  
  
## <a name="remarks"></a>備註  
 當 SET QUOTED_IDENTIFIER 是 ON 時，您可以用雙引號來分隔識別碼，文字則必須用單引號來分隔。 當 SET QUOTED_IDENTIFIER 是 OFF 時，識別碼不能附加引號，且必須遵照所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼規則。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。 文字可以用單引號或雙引號來分隔。  
  
 當 SET QUOTED_IDENTIFIER 是 ON (預設值) 時，用雙引號來分隔的所有字串都會解譯為物件識別碼。 因此，附加引號的識別碼不需要遵照 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的識別碼規則。 它們可以是保留關鍵字，也可以包括 [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別碼通常不接受的字元。 文字字串運算式不能用雙引號來分隔；您必須用單引號來括住文字字串。 如果單引號 (**'**) 是一部分的常值字串，它可由兩個單引號 (**"**)。 當資料庫中的物件名稱使用保留關鍵字時，SET QUOTED_IDENTIFIER 必須是 ON。  
  
 當 SET QUOTED_IDENTIFIER 是 OFF 時，您可以用單引號或雙引號來分隔運算式中的文字字串。 如果用雙引號來分隔文字字串，字串便可以包含內嵌的單引號，如撇號。  
  
 當您建立或變更計算資料行索引或索引檢視時，SET QUOTED_IDENTIFIER 也必須是 ON。 如果 SET QUOTED_IDENTIFIER 是 OFF，含計算資料行索引的資料表或索引檢視之 CREATE、UPDATE、INSERT 和 DELETE 陳述式會失敗。 計算資料行上使用索引檢視表和索引的必要 SET 選項設定的相關資訊，請參閱"考量當您使用 SET 陳述式 」，在[SET 陳述式 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-statements-transact-sql.md).  
  
 當您要建立篩選索引時，SET QUOTED_IDENTIFIER 必須是 ON。  
  
 當您叫用 XML 資料類型方法時，SET QUOTED_IDENTIFIER 必須是 ON。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]都會自動將 QUOTED_IDENTIFIER 設為 ON，連接時。 您可以在 ODBC 資料來源、ODBC 連接屬性或 OLE DB 連接屬性中設定這個項目。 起始於 DB-Library 應用程式的連接之 SET QUOTED_IDENTIFIER 預設值是 OFF。  
  
 當建立資料表時，一律會在資料表的中繼資料中，將 QUOTED IDENTIFIER 選項儲存成 ON，即使建立資料表時，將選項設成 OFF，也是如此。  
  
 當建立預存程序時，會擷取 SET QUOTED_IDENTIFIER 和 SET ANSI_NULLS 設定，這個預存程序的後續引動過程都會使用這些設定。  
  
 當在預存程序內執行時，不會變更 SET QUOTED_IDENTIFIER 的設定。  
  
 當 SET ANSI_DEFAULTS 是 ON 時，會啟用 SET QUOTED_IDENTIFIER。  
  
 另外，SET QUOTED_IDENTIFIER 也對應於 ALTER DATABASE 的 QUOTED_IDENTIFIER 設定。 如需有關資料庫設定的詳細資訊，請參閱[ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 SET QUOTED_IDENTIFIER 是在剖析階段會生效，而且只會影響剖析時，無法執行查詢。  
  
 最上層的特定批次剖析開始的 QUOTED_IDENTIFIER 使用工作階段的目前設定。  因為批次的剖析將變更剖析行為，從該點上，SET QUOTED_IDENTIFIER 的任何項目，並將其儲存該工作階段的設定。  因此剖析和執行批次之後，工作階段的 QUOTED_IDENTIFER 設定會根據批次中最後一個出現的 SET QUOTED_IDENTIFIER 設定。  
 靜態 SQL 預存程序會剖析為批次建立或更改預存程序的作用中使用的 QUOTED_IDENTIFIER 設定。  當做靜態 SQL 的預存程序主體中出現時，SET QUOTED_IDENTIFIER 沒有任何作用。  
  
 使用 sp_executesql 或 exec （） 的巢狀批次剖析開始使用工作階段的 QUOTED_IDENTIFIER 設定。  如果巢狀的批次是在剖析使用預存程序的 QUOTED_IDENTIFIER 設定會啟動預存程序內。  如巢狀的批次會剖析 SET QUOTED_IDENTIFIER 的任何項目將會變更剖析行為從該點上，但不是會更新工作階段的 QUOTED_IDENTIFIER 設定。  
  
 使用方括號**[**和**]**來分隔識別碼中，不會受到 QUOTED_IDENTIFIER 設定。  
  
 若要檢視此設定的目前設定，請執行下列查詢。  
  
```  
DECLARE @QUOTED_IDENTIFIER VARCHAR(3) = 'OFF';  
IF ( (256 & @@OPTIONS) = 256 ) SET @QUOTED_IDENTIFIER = 'ON';  
SELECT @QUOTED_IDENTIFIER AS QUOTED_IDENTIFIER;  
  
```  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-quoted-identifier-setting-and-reserved-word-object-names"></a>A. 使用引號識別碼設定及保留字物件名稱  
 下列範例會顯示 `SET QUOTED_IDENTIFIER` 設定必須是 `ON`，且資料表名稱中的關鍵字必須用雙引號括住，才能建立和使用含保留字名稱的物件。  
  
```  
SET QUOTED_IDENTIFIER OFF  
GO  
-- An attempt to create a table with a reserved keyword as a name  
-- should fail.  
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);  
GO  
  
SET QUOTED_IDENTIFIER ON;  
GO  
  
-- Will succeed.  
CREATE TABLE "select" ("identity" INT IDENTITY NOT NULL, "order" INT NOT NULL);  
GO  
  
SELECT "identity","order"   
FROM "select"  
ORDER BY "order";  
GO  
  
DROP TABLE "SELECT";  
GO  
  
SET QUOTED_IDENTIFIER OFF;  
GO  
```  
  
### <a name="b-using-the-quoted-identifier-setting-with-single-and-double-quotation-marks"></a>B. 搭配單引號和雙引號來使用引號識別碼設定  
 下列範例會顯示在 `SET QUOTED_IDENTIFIER` 設為 `ON` 和 `OFF` 的字串運算式中，單引號和雙引號的使用方式。  
  
```  
SET QUOTED_IDENTIFIER OFF;  
GO  
USE AdventureWorks2012;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'Test')  
   DROP TABLE dbo.Test;  
GO  
USE AdventureWorks2012;  
CREATE TABLE dbo.Test (ID INT, String VARCHAR(30)) ;  
GO  
  
-- Literal strings can be in single or double quotation marks.  
INSERT INTO dbo.Test VALUES (1, "'Text in single quotes'");  
INSERT INTO dbo.Test VALUES (2, '''Text in single quotes''');  
INSERT INTO dbo.Test VALUES (3, 'Text with 2 '''' single quotes');  
INSERT INTO dbo.Test VALUES (4, '"Text in double quotes"');  
INSERT INTO dbo.Test VALUES (5, """Text in double quotes""");  
INSERT INTO dbo.Test VALUES (6, "Text with 2 """" double quotes");  
GO  
  
SET QUOTED_IDENTIFIER ON;  
GO  
  
-- Strings inside double quotation marks are now treated   
-- as object names, so they cannot be used for literals.  
INSERT INTO dbo."Test" VALUES (7, 'Text with a single '' quote');  
GO  
  
-- Object identifiers do not have to be in double quotation marks  
-- if they are not reserved keywords.  
SELECT ID, String   
FROM dbo.Test;  
GO  
  
DROP TABLE dbo.Test;  
GO  
  
SET QUOTED_IDENTIFIER OFF;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ID          String 
 ----------- ------------------------------ 
 1           'Text in single quotes' 
 2           'Text in single quotes' 
 3           Text with 2 '' single quotes 
 4           "Text in double quotes" 
 5           "Text in double quotes" 
 6           Text with 2 "" double quotes 
 7           Text with a single ' quote
 ```  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [sp_rename &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)  
  
  
