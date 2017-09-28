---
title: "DATETIME2FROMPARTS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4ad800c684bcf69a52828969ca816a135901280
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

傳回**datetime2**具有指定的有效位數及指定的日期和時間值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>引數  
*年份*  
指定年份的整數運算式。
  
*月份*  
指定月份的整數運算式。
  
*一天*  
指定日期的整數運算式。
  
 *小時*  
指定小時的整數運算式。
  
*分鐘*指定分鐘的整數運算式。
  
*seconds*  
指定秒的整數運算式。
  
*分數*  
指定分數的整數運算式。
  
*有效位數*  
指定的有效位數的整數常值**datetime2**會傳回值。
  
## <a name="return-types"></a>傳回型別
**datetime2 (** *精確度* **)**
  
## <a name="remarks"></a>備註  
**DATETIME2FROMPARTS**傳回完整初始化**datetime2**值。 如果引數無效，將會引發錯誤。 如果要求的引數為 null，即會傳回 null。 不過，如果*精確度*引數為 null，則會引發錯誤。
  
*分數*引數取決於*精確度*引數。 例如，如果*精確度*為 7，則每個分數即表示 100 奈秒; 如果*精確度*為 3，則每個分數即表示 1 毫秒。 如果值*精確度*是零，則值*分數*也必須為零，否則會引發錯誤。
  
函數可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器和更新版伺服器上以遠端方式進行。 它在版本低於 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的伺服器上無法以遠端方式運作。
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小數部分的簡單範例  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 含秒的小數部分的範例  
下列範例示範如何使用*分數*和*精確度*參數：
  
1.  當*分數*的值為 5 和*精確度*然後的值具有值為 1，*分數*代表 5/10 秒。  
  
2.  當*分數*的值為 50 和*精確度*然後的值具有值為 2，*分數*表示 50/100 的第二個。  
  
3.  當*分數*的值為 500 和*精確度*然後的值具有值為 3，*分數*表示 500/1000 秒。  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example-without-fractions-of-a-second"></a>C. 不包含秒的小數部分的簡單範例  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="d-example-with-fractions-of-a-second"></a>D. 含秒的小數部分的範例  
下列範例示範如何使用*分數*和*精確度*參數：
1.  當*分數*的值為 5 和*精確度*然後的值具有值為 1，*分數*代表 5/10 秒。  
1.   當*分數*的值為 50 和*精確度*然後的值具有值為 2，*分數*表示 50/100 的第二個。  
1.   當*分數*的值為 500 和*精確度*然後的值具有值為 3，*分數*表示 500/1000 秒。  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  


