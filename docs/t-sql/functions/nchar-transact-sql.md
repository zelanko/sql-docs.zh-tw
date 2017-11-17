---
title: "NCHAR (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- nchar
- nchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- NCHAR function
- Unicode [SQL Server], NCHAR function
ms.assetid: 68cefc68-7c4f-4326-80c1-300f90cf19db
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: b70c591517177ad9febd1d0d9873a41192bf9414
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="nchar-transact-sql"></a>NCHAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  依照 Unicode 標準所定義，傳回含指定之整數碼的 Unicode 字元。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
NCHAR ( integer_expression )  
```  
  
## <a name="arguments"></a>引數  
 *integer_expression*  
 如果資料庫的定序不包含增補字元 (SC) 旗標，這會是從 0 到 65535 (0 到 0xFFFF) 的正整數。 如果指定了這個範圍以外的值，便會傳回 NULL。 如需補充字元的詳細資訊，請參閱[Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  
 如果資料庫的定序支援增補字元 (SC) 旗標，這會是從 0 到 1114111 (0 到 0x10FFFF) 的正整數。 如果指定了這個範圍以外的值，便會傳回 NULL。  
  
## <a name="return-types"></a>傳回類型  
 **nchar(1)**預設資料庫定序不支援補充字元時。  
  
 **nvarchar(2)**當預設資料庫定序支援增補字元。  
  
 如果參數*clause><*在於 0-0xFFFF 範圍，就會傳回只有一個字元。 對於較高值，NCHAR 會傳回對應的 Surrogate 字組。 請勿使用 `NCHAR(<High surrogate>) + NCHAR(\<Low Surrogate>)` 建構 Surrogate 字組。 而應使用支援增補字元的資料庫定序，然後為 Surrogate 字組指定 Unicode 字碼指標。 下列範例示範建構 Surrogate 字組的舊有樣式方法，以及指定 Unicode 字碼指標的慣用方法。  
  
```  
CREATE DATABASE test COLLATE Finnish_Swedish_100_CS_AS_SC;  
DECLARE @d nvarchar(10) = N'ࣅ炙   
-– Old style method.  
SELECT NCHAR(0xD84C) + NCHAR(0xDD7F);   
  
-- Preferred method.   
SELECT NCHAR(143743);   
  
-- Alternative preferred method.  
SELECT NCHAR(UNICODE(@d));    
```  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-nchar-and-unicode"></a>A. 使用 NCHAR 和 UNICODE  
 下列範例會利用 `UNICODE` 和 `NCHAR` 函數來列印 `UNICODE` 字元字串第二個字元的 `NCHAR` 值和 `København` (Unicode 字元)，以及列印實際的第二個字元 `ø`。  
  
```  
DECLARE @nstring nchar(8);  
SET @nstring = N'København';  
SELECT UNICODE(SUBSTRING(@nstring, 2, 1)),   
   NCHAR(UNICODE(SUBSTRING(@nstring, 2, 1)));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
248         ø  
(1 row(s) affected)  
```  
  
### <a name="b-using-substring-unicode-convert-and-nchar"></a>B. 使用 SUBSTRING、UNICODE、CONVERT 和 NCHAR  
 下列範例會利用 `SUBSTRING`、`UNICODE`、`CONVERT` 和 `NCHAR` 函數來列印 `København` 字串中的字元數目、Unicode 字元，以及各字元的 UNICODE 值。  
  
```  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(9);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.  
-- Notice that there is an N before the start of the string. This   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'København';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
   BEGIN  
   SELECT @position,   
      NCHAR(UNICODE(SUBSTRING(@nstring, @position, 1))),  
      CONVERT(NCHAR(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1))  
   SELECT @position = @position + 1  
   END;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ---- ----------------- -----------   
1           K    K                 75  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
2           ø    ø                 248  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
3           b    b                 98  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
4           e    e                 101  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
5           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
6           h    h                 104  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
7           a    a                 97  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
8           v    v                 118  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
9           n    n                 110  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
10          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
11          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
12          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
13          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
14          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
15          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
16          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
17          NULL                   NULL  
  
(1 row(s) affected)  
  
----------- ---- ----------------- -----------   
18          NULL                   NULL  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [UNICODE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/unicode-transact-sql.md)  
  
  


