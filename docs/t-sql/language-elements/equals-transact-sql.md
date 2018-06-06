---
title: = (等於) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- =
- = (Equals)
- Equals
- =_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- equals operator (=)
- = (equals operator)
ms.assetid: 18885245-5f55-4831-8f0b-7f2a3e82e246
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 77947f8263b66f1b7f26e8ee5a5d52a4d019aeb2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="-equals-transact-sql"></a>= (等於) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  比較 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中兩個運算式是否相等 (比較運算子)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression = expression  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 這是任何有效的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 如果運算式的資料類型不同，一個運算式的資料類型必須能夠隱含地轉換成另一運算式的資料類型。 轉換會以[資料類型優先順序](../../t-sql/data-types/data-type-precedence-transact-sql.md)的規則為基礎。  
  
## <a name="result-types"></a>結果類型  
 布林  
  
## <a name="remarks"></a>Remarks  
 當您比較兩個 NULL 運算式時，結果會隨著 `ANSI_NULLS` 設定而不同：  
  
-   如果將 `ANSI_NULLS` 設為 ON，結果會是 NULL，依照 ANSI 慣例，NULL (或未知) 值不等於另一個 NULL 或未知值。  
  
-   如果將 `ANSI_NULLS` 設為 OFF，NULL 與 NULL 的比較結果便是 TRUE。  

如需詳細資訊，請參閱 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)。
  
 任何種類的 NULL 值 (未知) 與非 NULL 值比較，一律會產生 FALSE。  
  
  
## <a name="examples"></a>範例  
  
### <a name="a-using--in-a-simple-query"></a>A. 在簡單的查詢中使用 =  
 下列範例會使用等於運算子傳回 `HumanResources.Department` 中，其 `GroupName` 資料行的值等於 'Manufacturing' 這個字的所有資料列。  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE GroupName = 'Manufacturing';  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
DepartmentID Name  
------------ --------------------------------------------------  
7            Production  
8            Production Control  
  
(2 row(s) affected)  
  
```  
  
### <a name="b-comparing-null-and-non-null-values"></a>B. 比較 NULL 和非 NULL 值  
 下列範例會利用等於 (`=`) 和不等於 (`<>`) 比較運算子，與資料表中的 `NULL` 和非 Null 值比較。 這個範例也示範 `IS NULL` 不會受到 `SET ANSI_NULLS` 設定的影響。  
  
```  
-- Create table t1 and insert 3 rows.  
CREATE TABLE dbo.t1 (a INT NULL);  
INSERT INTO dbo.t1 VALUES (NULL),(0),(1);  
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
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Testing default setting  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
a  
-----------  
0  
1  
  
(2 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
Testing ANSI_NULLS ON  
a  
-----------  
  
(0 row(s) affected)  
  
a  
-----------  
  
(0 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
Testing SET ANSI_NULLS OFF  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
a  
-----------  
0  
1  
  
(2 row(s) affected)  
  
a  
-----------  
NULL  
  
(1 row(s) affected)  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
