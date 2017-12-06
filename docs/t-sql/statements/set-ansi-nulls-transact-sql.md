---
title: "SET ANSI_NULLS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_ANSI_NULLS_TSQL
- ANSI_NULLS
- SET ANSI_NULLS
- ANSI_NULLS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- SET ANSI_NULLS statement
- not equal to operator (<>)
- ANSI_NULLS option
- equals operator (=)
- null values [SQL Server], comparison operators
- comparison operators [SQL Server], null values
ms.assetid: aae263ef-a3c7-4dae-80c2-cc901e48c755
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a6ef51bb13ae7372175a390a3d8c5509550a3ad1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="set-ansinulls-transact-sql"></a>SET ANSI_NULLS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  指定在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中搭配 Null 值一起使用時，等於 (=) 和不等於 (<>) 比較運算子的 ISO 標準行為。  
  
> [!IMPORTANT]  
>  未來版本中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 ANSI_NULLS 是 ON，以及任何明確地將選項設為 OFF 的應用程式會產生錯誤。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>語法

```
-- Syntax for SQL Server

SET ANSI_NULLS { ON | OFF }
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_NULLS ON
```

## <a name="remarks"></a>備註  
 當 SET ANSI_NULLS 是 ON 時，SELECT 陳述式，使用 WHERE *column_name* = **NULL**傳回零個資料列，即使有 null 值在*column_name*。 SELECT 陳述式，使用 WHERE *column_name* <> **NULL**傳回零個資料列，即使在非 null 值*column_name*。  
  
 當 SET ANSI_NULLS 是 OFF 時，等於 (=) 和不等於 (<>) 比較運算子並不遵照 ISO 標準。 SELECT 陳述式，使用 WHERE *column_name* = **NULL**傳回中具有 null 值的資料列*column_name*。 SELECT 陳述式，使用 WHERE *column_name* <> **NULL**傳回資料行中有非 null 值的資料列。 此外，SELECT 陳述式，使用 WHERE *column_name* <> *XYZ_value*傳回所有資料列不*XYZ_value*並不是 NULL。  
  
 當 SET ANSI_NULLS 是 ON 時，所有對於 Null 值的比較都會得出 UNKNOWN。 當 SET ANSI_NULLS 是 OFF 時，如果資料值是 NULL，所有對於 Null 值的資料比較都會得出 TRUE。 如果未指定 SET ANSI_NULLS，就會套用目前資料庫的 ANSI_NULLS 選項設定。 如需有關 ANSI_NULLS 資料庫選項的詳細資訊，請參閱[ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 只有在一個比較運算元是 NULL 變數或常值 NULL 變數時，SET ANSI_NULLS ON 才會影響比較。 如果比較的兩端是資料行或複合運算式，設定就不會影響比較。  
  
 若要使指令碼的運作能夠符合預期，不論 ANSI_NULLS 資料庫選項或 SET ANSI_NULLS 設定為何，請在可能含有 Null 值的比較中，使用 IS NULL 和 IS NOT NULL。  
  
 SET ANSI_NULLS 應該設為 ON，以便執行分散式查詢。  
  
 當您建立或變更計算資料行索引或索引檢視表時，SET ANSI_NULLS 也必須是 ON。 如果 SET ANSI_NULLS 是 OFF，含計算資料行索引的資料表或索引檢視之任何 CREATE、UPDATE、INSERT 和 DELETE 陳述式會失敗。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會傳回錯誤，列出違反必要的值的所有 SET 選項。 此外，當您執行 SELECT 陳述式，如果 SET ANSI_NULLS 是 OFF，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會忽略針對計算資料行或檢視表的索引值，並解決好像沒有這類索引的資料表或檢視表的 select 作業。  
  
> [!NOTE]  
>  ANSI_NULLS 是處理計算資料行索引或索引檢視表時，必須設成必要選項的七個 SET 選項之一。 ANSI_PADDING、ANSI_WARNINGS、ARITHABORT、QUOTED_IDENTIFIER 和 CONCAT_NULL_YIELDS_NULL 等選項也必須設成 ON，NUMERIC_ROUNDABORT 必須設成 OFF。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動將 ansi_nulls 設為 ON，連接時。 您可以在 ODBC 資料來源、ODBC 連接屬性中設定這項設定，或在應用程式連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之前所設定的 OLE DB 連接屬性中設定這項設定。 SET ANSI_NULLS 的預設值為 OFF。  
  
 當 SET ANSI_DEFAULTS 是 ON 時，會啟用 SET ANSI_NULLS。  
  
 SET ANSI_NULLS 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 若要檢視這項設定的目前設定，請執行下列查詢：
  
```  
DECLARE @ANSI_NULLS VARCHAR(3) = 'OFF';  
IF ( (32 & @@OPTIONS) = 32 ) SET @ANSI_NULLS = 'ON';  
SELECT @ANSI_NULLS AS ANSI_NULLS;  
  
```  
  
## <a name="permissions"></a>Permissions  
 需要 public 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會利用等於 (`=`) 和不等於 (`<>`) 比較運算子，與資料表中的 `NULL` 和非 Null 值比較。 這個範例也顯示`IS NULL`不會受到`SET ANSI_NULLS`設定。  
  
```  
-- Create table t1 and insert values.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 values (NULL),(0),(1);  
GO  
  
-- Print message and perform SELECT statements.  
PRINT 'Testing default setting';  
DECLARE @varname int;   
SET @varname = NULL;  
  
SELECT a  
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to ON and test.  
PRINT 'Testing ANSI_NULLS ON';  
SET ANSI_NULLS ON;  
GO  
DECLARE @varname int;  
SET @varname = NULL  
  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- SET ANSI_NULLS to OFF and test.  
PRINT 'Testing SET ANSI_NULLS OFF';  
SET ANSI_NULLS OFF;  
GO  
DECLARE @varname int;  
SET @varname = NULL;  
SELECT a   
FROM t1   
WHERE a = @varname;  
  
SELECT a   
FROM t1   
WHERE a <> @varname;  
  
SELECT a   
FROM t1   
WHERE a IS NULL;  
GO  
  
-- Drop table t1.  
DROP TABLE dbo.t1;  
  
```  
  
## <a name="see-also"></a>請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SESSIONPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/sessionproperty-transact-sql.md)   
 [= &#40;Equals &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [如果...其他 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [&#60; &#62;&#40;不等於 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  
