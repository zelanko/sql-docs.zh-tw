---
title: "DATEDIFF (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
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
- DATEDIFF_TSQL
- DATEDIFF
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATEDIFF function [SQL Server]
- time [SQL Server], crossed boundaries
- differences in date and time [SQL Server]
- counting crossed date time boundaries [SQL Server]
- date and time [SQL Server], DATEDIFF
- dates [SQL Server], crossed boundaries
- boundary differences date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- interval dates [SQL Server]
- time [SQL Server], functions
- crossing date time boundaries [SQL Server]
- calculating dates times [SQL Server]
ms.assetid: eba979f2-1a8d-4cce-9d75-b74f9b519b37
caps.latest.revision: 52
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: dba834b51bab48c2bd30d1bbbb4abe11694ab321
ms.contentlocale: zh-tw
ms.lasthandoff: 10/05/2017

---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回指定的計數 （帶正負號的整數） *datepart*界限跨越指定*startdate*和*enddate*。
  
針對較大的差異，請參閱[DATEDIFF_BIG &#40;TRANSACT-SQL &#41;](../../t-sql/functions/datediff-big-transact-sql.md). 如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>引數  
*日期部份*  
是的一部分*startdate*和*enddate*指定跨越界限的類型。 下表列出所有有效*datepart*引數。 使用者自訂變數對等項目無效。
  
|*日期部份*|縮寫|  
|---|---|
|**年份**|**yy、 yyyy**|  
|**季**|**qq、 q**|  
|**月份**|**mm、 m**|  
|**dayofyear**|**dy、 y**|  
|**一天**|**dd、 d**|  
|**週**|**wk、 ww**|  
|**小時**|**hh**|  
|**分鐘**|**mi、 n**|  
|**第二個**|**ss、 s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**奈秒**|**ns**|  
  
*startdate*  
運算式是可解析成**時間**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是運算式、 資料行運算式、 使用者定義變數或字串常值。 *startdate*會減去*enddate*。
  
若要避免模糊不清，請使用四位數年份。 兩位數年份的相關資訊，請參閱[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
*結束日期*  
請參閱*startdate*。
  
## <a name="return-type"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
  
-   每個*datepart*及其縮寫都會傳回相同的值。  
  
如果傳回的值超出範圍**int** (介於-2147483648 到 + 2147483647)，則會傳回錯誤。 如**毫秒**，之間的最大差異*startdate*和*enddate*是 24 天、 20 小時 31 分鐘和 23.647 秒。 如**第二個**，最大的差異是 68 年。
  
如果*startdate*和*enddate*同時指派時間值和*datepart*不是時間*datepart*，就會傳回 0。
  
時區位移元件*startdate*或*endate*不會用於計算傳回的值。
  
因為[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)的精確度只有到分鐘，當**smalldatetime**值用於*startdate*或*enddate*、 秒和毫秒為單位永遠會設定為 0 的傳回值。
  
如果只將時間值指派給日期資料類型的變數，則遺漏日期部分的值設定為預設值： 1900年-01-01。 如果只是日期值指派給時間或日期的資料類型的變數，遺漏時間部分的值會設定為預設值： 00:00:00。 如果有任一個*startdate*或*enddate*只有時間部分和其他只有日期部分、 遺漏的時間和日期部分設定為預設值。
  
如果*startdate*和*enddate*是不同的日期資料類型，另一個有更多的時間部分或小數秒數有效位數超過另，其他遺失的組件會設定為 0。
  
## <a name="datepart-boundaries"></a>datepart 界限  
下列陳述式具有相同*startdate*和相同*endate*。 這些日期都很接近而且時間差距為 .0000001 秒。 之間的差異*startdate*和*endate*每個陳述式中已超過一個日曆或時間界限的其*datepart*。 每個陳述式都會傳回 1。 如果這個範例會使用不同的年份，如果兩個*startdate*和*endate*位於相同的日曆週的傳回值**週**就是 0。
  
```sql
SELECT DATEDIFF(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>備註  
DATEDIFF 可用於選取清單、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
DATEDIFF 會隱含地將轉換為字串常值**datetime2**型別。 這表示，將日期當做字串傳遞時，DATEDIFF 不支援 YDM 格式。 您必須明確地將字串轉換成**datetime**或**smalldatetime**類型才能使用 YDM 格式。
  
指定 SET DATEFIRST 對 DATEDIFF 沒有任何作用。 DATEDIFF 一定會使用星期天當做一週的第一天，以確保此函數具決定性。
  
## <a name="examples"></a>範例  
下列範例會使用不同類型的運算式做為引數*startdate*和*enddate*參數。
  
### <a name="a-specifying-columns-for-startdate-and-enddate"></a>A. 指定 startdate 和 enddate 的資料行  
下列範例會計算資料表中兩個資料行之間的日期已跨越的天數界限。
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="b-specifying-user-defined-variables-for-startdate-and-enddate"></a>B. 指定 startdate 和 enddate 的使用者自訂變數  
下列範例會使用使用者定義的變數做為引數*startdate*和*enddate*。
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. 指定 startdate 和 enddate 的純量系統函數  
下列範例會使用純量系統函數做為引數*startdate*和*enddate*。
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. 指定 startdate 和 enddate 的純量子查詢和純量函數  
下列範例會使用純量子查詢和純量函數做為引數*startdate*和*enddate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,(SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. 指定 startdate 和 enddate 的常數  
下列範例會使用字元常數做為引數*startdate*和*enddate*。
  
```sql
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. 指定 enddate 的數值運算式和純量系統函數  
下列範例使用數值運算式， `(GETDATE ()+ 1)`，和純量系統函數`GETDATE`和`SYSDATETIME`，做為引數*enddate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', GETDATE()+ 1)   
    AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635', DATEADD(day,1,SYSDATETIME())) AS NumberOfDays  
FROM Sales.SalesOrderHeader;  
GO  
```  
  
### <a name="g-specifying-ranking-functions-for-startdate"></a>G. 指定 startdate 的排名函數  
下列範例會使用排名函數做為引數*startdate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName  
    ,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson s   
    INNER JOIN Person.Person p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
### <a name="h-specifying-an-aggregate-window-function-for-startdate"></a>H. 指定 startdate 的彙總視窗函數  
下列範例會使用彙總視窗函數的引數為*startdate*。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT soh.SalesOrderID, sod.ProductID, sod.OrderQty,soh.OrderDate  
    ,DATEDIFF(day,MIN(soh.OrderDate)   
        OVER(PARTITION BY soh.SalesOrderID),SYSDATETIME() ) AS 'Total'  
FROM Sales.SalesOrderDetail sod  
    INNER JOIN Sales.SalesOrderHeader soh  
        ON sod.SalesOrderID = soh.SalesOrderID  
WHERE soh.SalesOrderID IN(43659,58918);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
下列範例會使用不同類型的運算式做為引數*startdate*和*enddate*參數。
  
### <a name="i-specifying-columns-for-startdate-and-enddate"></a>I. 指定 startdate 和 enddate 的資料行  
下列範例會計算資料表中兩個資料行之間的日期已跨越的天數界限。
  
```sql
CREATE TABLE dbo.Duration (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT TOP(1) DATEDIFF(day,startDate,endDate) AS Duration  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
### <a name="j-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>J. 指定 startdate 和 enddate 的純量子查詢和純量函數  
下列範例會使用純量子查詢和純量函數做為引數*startdate*和*enddate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,(SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>K. 指定 startdate 和 enddate 的常數  
下列範例會使用字元常數做為引數*startdate*和*enddate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>L. 指定 startdate 的排名函數  
下列範例會使用排名函數做為引數*startdate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        DepartmentName),SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>M. 指定 startdate 的彙總視窗函數  
下列範例會使用彙總視窗函數的引數為*startdate*。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName  
    ,DATEDIFF(year,MAX(HireDate)  
             OVER (PARTITION BY DepartmentName),SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>另請參閱
[DATEDIFF_BIG &#40;TRANSACT-SQL &#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



