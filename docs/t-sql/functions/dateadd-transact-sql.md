---
title: "DATEADD (TRANSACT-SQL) |Microsoft 文件"
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
- DATEADD
- DATEADD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- add interval to date or time [SQL Server]
- subtract interval from date or time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], intervals
- date and time [SQL Server], DATEADD
- DATEADD function [SQL Server]
ms.assetid: 89c5ae32-89c6-47e1-979e-15d97908b9f1
caps.latest.revision: 71
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6a90b51a1ef2156a2a05b8d3dd4e15111872edf6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dateadd-transact-sql"></a>DATEADD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回指定*日期*具有指定*數目*間隔 （帶正負號的整數） 加入至指定*datepart*的*日期*。
  
如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>引數  
*日期部份*  
是的一部分*日期*的**整數***數目*加入。 下表列出所有有效*datepart*引數。 使用者自訂變數對等項目無效。
  
|*日期部份*|縮寫|  
|---|---|
|**年份**|**yy**， **yyyy**|  
|**季**|**qq**， **q**|  
|**月份**|**mm**， **m**|  
|**dayofyear**|**dy**， **y**|  
|**一天**|**dd**， **d**|  
|**週**|**wk**， **ww**|  
|**週間日**|**dw**， **w**|  
|**小時**|**hh**|  
|**分鐘**|**mi**，**n**|  
|**第二個**|**ss**， **s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**奈秒**|**ns**|  
  
*number*  
運算式是可解析成[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)加入至*datepart*的*日期*。 使用者自訂的變數有效。  
如果您指定了含有十進位小數的值，該小數就會被截斷而且不會四捨五入。
  
*date*  
運算式是可解析成**時間**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是運算式、 資料行運算式、 使用者定義的變數或字串常值。 如果運算式是字串常值，它必須解析成**datetime**。 若要避免模糊不清，請使用四位數年份。 如需兩位數年份，請參閱[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-types"></a>傳回型別
傳回資料型別是資料型別*日期*引數，但字串常值除外。
傳回的資料類型的字串常值是**datetime**。 如果字串常值的秒數小數位數超過三個位置 (.nnn)，或者包含時區位移部分，就會引發錯誤。
  
## <a name="return-value"></a>傳回值  
  
## <a name="datepart-argument"></a>datepart 引數  
**dayofyear**，**天**，和**工作日**傳回相同的值。
  
每個*datepart*及其縮寫都會傳回相同的值。
  
如果*datepart*是**月份**和*日期*月有更多的天數比傳回月份和*日期*日期傳回月份，在不存在會傳回傳回月份的最後一天。 例如，九月有 30 天。因此，下列陳述式會傳回 2006-09-30 00:00:00.000：
  
```sql
SELECT DATEADD(month, 1, '2006-08-30');
SELECT DATEADD(month, 1, '2006-08-31');
```
  
## <a name="number-argument"></a>number 引數  
*數目*引數不能超過範圍**int**。下列陳述式的引數*數目*超過範圍**int** 1。 系統會傳回下列錯誤訊息："`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '2006-07-31');  
SELECT DATEADD(year,-2147483649, '2006-07-31');  
```  
  
## <a name="date-argument"></a>date 引數  
*日期*引數不得遞增為其資料類型的範圍以外的值。 下列陳述式，*數目*值加入至*日期*值超過範圍*日期*資料型別。 系統會傳回下列錯誤訊息："`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`."
  
```sql
SELECT DATEADD(year,2147483647, '2006-07-31');  
SELECT DATEADD(year,-2147483647, '2006-07-31');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>smalldatetime date 和 second 或小數秒數 datepart 的傳回值  
秒數部分[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)值一定是 00。 如果*日期*是**smalldatetime**，則適用下列步驟：
-   如果*datepart*是**第二個**和*數目*是法力 + 29，-30 之間會執行任何加法。  
-   如果*datepart*是**第二個**和*數目*較少比 30 或多個法力 + 29，從一分鐘開始執行加法。  
-   如果*datepart*是**毫秒**和*數目*是介於-30001 與 + 29998，會執行任何加法。  
-   如果*datepart*是**毫秒**和*數目*小於-30001 或大於 + 29998，從一分鐘開始執行加法。  
  
## <a name="remarks"></a>備註  
DATEADD 可用於 SELECT\<清單 >，其中 HAVING、 GROUP BY 和 ORDER BY 子句。
  
## <a name="fractional-seconds-precision"></a>小數秒數有效位數
若是*datepart*的**微秒**或**奈秒**如*日期*資料型別**smalldatetime**，**日期**，和**datetime**不允許。
  
毫秒具有小數位數 3 (.123)，微秒具有小數位數 6 (.123456)，奈秒具有小數位數 9 (.123456789)。 **時間**， **datetime2**，和**datetimeoffset**資料型別有最大的小數位數 7 (。 1234567)。 如果*datepart*是**奈秒**，*數目*之前的小數秒數必須 100*日期*增加。 A*數目*1 與 49 之間會向下捨入 0 到 50 到 99 的數字會捨入到 100。
  
下列陳述式加入*datepart*的**毫秒**，**微秒**，或**奈秒**。
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT '1 millisecond', DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT '2 milliseconds', DATEADD(millisecond,2,@datetime2)  
UNION ALL  
SELECT '1 microsecond', DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT '2 microseconds', DATEADD(microsecond,2,@datetime2)  
UNION ALL  
SELECT '49 nanoseconds', DATEADD(nanosecond,49,@datetime2)  
UNION ALL  
SELECT '50 nanoseconds', DATEADD(nanosecond,50,@datetime2)  
UNION ALL  
SELECT '150 nanoseconds', DATEADD(nanosecond,150,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1 millisecond     2007-01-01 13:10:10.1121111  
2 milliseconds    2007-01-01 13:10:10.1131111  
1 microsecond     2007-01-01 13:10:10.1111121  
2 microseconds    2007-01-01 13:10:10.1111131  
49 nanoseconds    2007-01-01 13:10:10.1111111  
50 nanoseconds    2007-01-01 13:10:10.1111112  
150 nanoseconds   2007-01-01 13:10:10.1111113  
```  
  
## <a name="time-zone-offset"></a>時區位移
不允許針對時區位移執行加法。
  
## <a name="examples"></a>範例  

### <a name="a-incrementing-datepart-by-an-interval-of-1"></a>A. 以 1 為間隔遞增 datepart  
下列陳述式為增量單位的每個*datepart* 1 為間隔。
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT 'year', DATEADD(year,1,@datetime2)  
UNION ALL  
SELECT 'quarter',DATEADD(quarter,1,@datetime2)  
UNION ALL  
SELECT 'month',DATEADD(month,1,@datetime2)  
UNION ALL  
SELECT 'dayofyear',DATEADD(dayofyear,1,@datetime2)  
UNION ALL  
SELECT 'day',DATEADD(day,1,@datetime2)  
UNION ALL  
SELECT 'week',DATEADD(week,1,@datetime2)  
UNION ALL  
SELECT 'weekday',DATEADD(weekday,1,@datetime2)  
UNION ALL  
SELECT 'hour',DATEADD(hour,1,@datetime2)  
UNION ALL  
SELECT 'minute',DATEADD(minute,1,@datetime2)  
UNION ALL  
SELECT 'second',DATEADD(second,1,@datetime2)  
UNION ALL  
SELECT 'millisecond',DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT 'microsecond',DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT 'nanosecond',DATEADD(nanosecond,1,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Year         2008-01-01 13:10:10.1111111  
quarter      2007-04-01 13:10:10.1111111  
month        2007-02-01 13:10:10.1111111  
dayofyear    2007-01-02 13:10:10.1111111  
day          2007-01-02 13:10:10.1111111  
week         2007-01-08 13:10:10.1111111  
weekday      2007-01-02 13:10:10.1111111  
hour         2007-01-01 14:10:10.1111111  
minute       2007-01-01 13:11:10.1111111  
second       2007-01-01 13:10:11.1111111  
millisecond  2007-01-01 13:10:10.1121111  
microsecond  2007-01-01 13:10:10.1111121  
nanosecond   2007-01-01 13:10:10.1111111  
```  
  
### <a name="b-incrementing-more-than-one-level-of-datepart-in-one-statement"></a>B. 在單一陳述式中遞增一個以上的 datepart 層級  
下列陳述式為增量單位的每個*datepart*所*數目*夠大，無法遞增下一個更高版本*datepart*的*日期*.
  
```sql
DECLARE @datetime2 datetime2;  
SET @datetime2 = '2007-01-01 01:01:01.1111111';  
--Statement                                 Result     
-------------------------------------------------------------------   
SELECT DATEADD(quarter,4,@datetime2);     --2008-01-01 01:01:01.110  
SELECT DATEADD(month,13,@datetime2);      --2008-02-01 01:01:01.110  
SELECT DATEADD(dayofyear,365,@datetime2); --2008-01-01 01:01:01.110  
SELECT DATEADD(day,365,@datetime2);       --2008-01-01 01:01:01.110  
SELECT DATEADD(week,5,@datetime2);        --2007-02-05 01:01:01.110  
SELECT DATEADD(weekday,31,@datetime2);    --2007-02-01 01:01:01.110  
SELECT DATEADD(hour,23,@datetime2);       --2007-01-02 00:01:01.110  
SELECT DATEADD(minute,59,@datetime2);     --2007-01-01 02:00:01.110  
SELECT DATEADD(second,59,@datetime2);     --2007-01-01 01:02:00.110  
SELECT DATEADD(millisecond,1,@datetime2); --2007-01-01 01:01:01.110  
```  
  
### <a name="c-using-expressions-as-arguments-for-the-number-and-date-parameters"></a>C. 使用運算式當做 number 和 date 參數的引數  
下列範例會使用不同類型的運算式做為引數*數目*和*日期*參數。 範例會使用 AdventureWorks 資料庫。
  
#### <a name="specifying-a-column-as-date"></a>指定資料行成為 date  
下列範例會將 `2` 天加入至 `OrderDate` 資料行中的每個值，以便衍生名為 `PromisedShipDate` 的新資料行。
  
```sql
SELECT SalesOrderID  
    ,OrderDate   
    ,DATEADD(day,2,OrderDate) AS PromisedShipDate  
FROM Sales.SalesOrderHeader;  
```  
  
以下為部分結果集。
  
```sql
SalesOrderID OrderDate               PromisedShipDate  
------------ ----------------------- -----------------------  
43659        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43660        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43661        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
...  
43702        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43703        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43704        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43705        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43706        2005-07-03 00:00:00.000 2005-07-05 00:00:00.000  
...  
43711        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
43712        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
...  
43740        2005-07-11 00:00:00.000 2005-07-13 00:00:00.000  
43741        2005-07-12 00:00:00.000 2005-07-14 00:00:00.000  
  
```  
  
#### <a name="specifying-user-defined-variables-as-number-and-date"></a>指定使用者自訂變數成為 number 和 date  
下列範例會指定使用者定義的變數做為引數*數目*和*日期*。
  
```sql
DECLARE @days int = 365,   
        @datetime datetime = '2000-01-01 01:01:01.111'; /* 2000 was a leap year */;  
SELECT DATEADD(day, @days, @datetime);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------------------  
2000-12-31 01:01:01.110  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-system-function-as-date"></a>指定純量系統函數成為 date  
下列範例會指定`SYSDATETIME`如*日期*。
  
```sql
SELECT DATEADD(month, 1, SYSDATETIME());  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------  
2013-02-06 14:29:59.6727944  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-subqueries-and-scalar-functions-as-number-and-date"></a>指定純量子查詢和純量函數成為 number 和 date  
下列範例會使用純量子查詢， `MAX(ModifiedDate)`，做為引數*數目*和*日期*。 `(SELECT TOP 1 BusinessEntityID FROM Person.Person)`會顯示如何選取數字參數的假造引數*數目*引數，從值清單。
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>指定數值運算式和純量系統函數成為 number 和 date  
下列範例使用數值運算式 (-`(10/2))`，[一元運算子](../../mdx/unary-operators.md)(`-`)、[算術運算子](../../mdx/arithmetic-operators.md)(`/`)，和純量系統函數 (`SYSDATETIME`) 做為引數*數目*和*日期*。
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>指定排名函數成為 number  
下列範例會使用排名函數做為引數*數目*。
  
```sql
SELECT p.FirstName, p.LastName  
    ,DATEADD(day,ROW_NUMBER() OVER (ORDER BY  
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
#### <a name="specifying-an-aggregate-window-function-as-number"></a>指定彙總視窗函數成為 number  
下列範例會使用彙總視窗函數的引數為*數目*。
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


