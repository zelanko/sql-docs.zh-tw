---
title: "UNICODE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- UNICODE
- UNICODE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first character of input expression [SQL Server]
- UNICODE function
- Unicode [SQL Server], UNICODE function
ms.assetid: 5e3c40b2-8401-4741-9f2a-bae70eaa4da6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: ce87bcab037ff99b7eaa03a443727db17db19b74
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="unicode-transact-sql"></a>UNICODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  依照 Unicode 標準所定義，傳回輸入運算式第一個字元的整數值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
UNICODE ( 'ncharacter_expression' )  
```  
  
## <a name="arguments"></a>引數  
 **'** *ncharacter_expression* **'**  
 是**nchar**或**nvarchar**運算式。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之前的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 版本中和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，UNICODE 函數會傳回 0 到 0xFFFF 範圍內的 UCS-2 字碼指標。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本中，使用 SC 定序時，UNICODE 會傳回在 0 到 0x10FFFF 範圍內的 UTF-16 字碼指標。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-unicode-and-the-nchar-function"></a>A. 使用 UNICODE 和 NCHAR 函數  
 下列範例會利用 `UNICODE` 和 `NCHAR` 函數來列印 `Åkergatan` 24 個字元字串中第一個字元的 UNICODE 值，以及列印實際的第一個字元 `Å`。  
  
```  
DECLARE @nstring nchar(12);  
SET @nstring = N'Åkergatan 24';  
SELECT UNICODE(@nstring), NCHAR(UNICODE(@nstring));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
197         Å  
```  
  
### <a name="b-using-substring-unicode-and-convert"></a>B. 使用 SUBSTRING、UNICODE 和 CONVERT  
 下列範例會利用 `SUBSTRING`、`UNICODE` 和 `CONVERT` 函數來列印 `Åkergatan 24` 字串中的字元數目、Unicode 字元，以及每個字元的 UNICODE 值。  
  
```  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(12);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.   
-- Notice that there is an N before the start of the string, which   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'Åkergatan 24';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
-- While these are still characters in the character string,  
   BEGIN;  
   SELECT @position,   
      CONVERT(char(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1));  
   SELECT @position = @position + 1;  
   END;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ----------------- -----------   
1           Å                 197           
  
----------- ----------------- -----------   
2           k                 107           
  
----------- ----------------- -----------   
3           e                 101           
  
----------- ----------------- -----------   
4           r                 114           
  
----------- ----------------- -----------   
5           g                 103           
  
----------- ----------------- -----------   
6           a                 97            
  
----------- ----------------- -----------   
7           t                 116           
  
----------- ----------------- -----------   
8           a                 97            
  
----------- ----------------- -----------   
9           n                 110           
  
----------- ----------------- -----------   
10                            32            
  
----------- ----------------- -----------   
11          2                 50            
  
----------- ----------------- -----------   
12          4                 52  
```  
  
## <a name="see-also"></a>另請參閱  
 [ASCII &#40;Transact-SQL&#41;](../../t-sql/functions/ascii-transact-sql.md)  
 [CHAR &#40;TRANSACT-SQL &#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40;TRANSACT-SQL &#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

