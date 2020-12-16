---
description: UNICODE (Transact-SQL)
title: UNICODE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9f3b9d166090d224c6af3743e832170b2300509
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97421633"
---
# <a name="unicode-transact-sql"></a>UNICODE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  依照 Unicode 標準所定義，傳回輸入運算式第一個字元的整數值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
UNICODE ( 'ncharacter_expression' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
**'** *ncharacter_expression* **'**  
這是 **nchar** 或 **nvarchar** 運算式。  
  
## <a name="return-types"></a>傳回型別  
**int**  
  
## <a name="remarks"></a>備註  
在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 之前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本與 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，UNICODE 函式會傳回範圍介於 000000 到 00FFFF 之間的 UCS-2 字碼元素，此範圍可代表 Unicode 基本多語平面 (BMP) 中的 65,535 個字元。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，當使用支援[補充字元 (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) 的定序時，UNICODE 會傳回範圍 000000 到 10FFFF 之間的 UTF-16 字碼元素。 如需 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 中 Unicode 支援的詳細資訊，請參閱[定序和 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn)。 
  
## <a name="examples"></a>範例  
  
### <a name="a-using-unicode-and-the-nchar-function"></a>A. 使用 UNICODE 和 NCHAR 函數  
 下列範例會利用 `UNICODE` 和 `NCHAR` 函數來列印 `Åkergatan` 24 個字元字串中第一個字元的 UNICODE 值，以及列印實際的第一個字元 `Å`。  
  
```sql  
DECLARE @nstring NCHAR(12);  
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
  
```sql  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position INT, @nstring NCHAR(12);  
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
WHILE @position <= LEN(@nstring)  
-- While these are still characters in the character string,  

BEGIN;  
   SELECT @position AS [position],   
      SUBSTRING(@nstring, @position, 1) AS [character],  
      UNICODE(SUBSTRING(@nstring, @position, 1)) AS [code_point];  
   SET @position = @position + 1;  
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
 [CHAR &#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  

