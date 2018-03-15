---
title: DATEDIFF (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: c7eaab4807f87aca3de9d4fb318c9069f5efdc67
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2018
---
# <a name="datediff-transact-sql"></a>DATEDIFF (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回跨越指定 *startdate* 和 *enddate* 之指定 *datepart* 界限的計數 (帶正負號的整數)。
  
針對較大的差異，請參閱 [DATEDIFF_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md)。 如需所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函數的概觀，請參閱[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATEDIFF ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>引數  
*datepart*  
這是指定所跨越之界限類型的 *startdate* 和 *enddate* 的一部分。 下表列出所有有效的 *datepart* 引數。 使用者自訂變數對等項目無效。
  
|*datepart*|縮寫|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*startdate*  
這是可解析成 **time**、**date**、**smalldatetime**、**datetime**、**datetime2** 或 **datetimeoffset** 值的運算式。 *date* 可以是運算式、資料行運算式、使用者定義的變數或字串常值。 *startdate* 會從 *enddate* 減去。
  
若要避免模糊不清，請使用四位數年份。 如需兩位數年份的詳細資訊，請參閱[設定兩位數年份的截止伺服器設定選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
*enddate*  
請參閱＜*startdate*＞。
  
## <a name="return-type"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
  
-   每個 *datepart* 及其縮寫都會傳回相同的值。  
  
如果傳回值超出 **int** 的範圍 (-2,147,483,648 到 +2,147,483,647)，便會傳回錯誤。 針對 **millisecond**，*startdate* 和 *enddate* 最大的差異為 24 天 20 小時 31 分鐘 23.647 秒。 針對 **second**，最大的差異為 68 年。
  
如果 *startdate* 和 *enddate* 都只獲指派時間值，且 *datepart* 不是時間 *datepart*，則會傳回 0。
  
*startdate* 或 *enddate* 的時區時差元件不會用於計算傳回值。
  
由於 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 的精確度只有到分鐘，因此當 **smalldatetime** 值用於 *startdate* 或 *enddate* 時，秒和毫秒就一律會在傳回值中設定為 0。
  
如果您只有將時間值指派給日期資料類型的變數，則遺漏日期部分的值就會設定為預設值：1900-01-01。 如果您只有將日期值指派給時間或日期資料類型的變數，則遺漏時間部分的值就會設定為預設值：00:00:00。 如果 *startdate* 或 *enddate* 其中之一只有時間部分，而另一個只有日期部分，則遺漏的時間和日期部分都會設定為預設值。
  
如果 *startdate* 和 *enddate* 具有不同的日期資料類型，而且其中一個項目的時間部分或小數秒數有效位數超過另一個項目，則另一個項目的遺漏部分就會設定為 0。
  
## <a name="datepart-boundaries"></a>datepart 界限  
下列陳述式具有相同的 *startdate* 和相同的 *enddate*。 這些日期都很接近而且時間差距為 .0000001 秒。 每個陳述式中 *startdate* 與 *enddate* 之間的差異會跨越其 *datepart* 的日曆或時間界限。 每個陳述式都會傳回 1。 如果這個範例使用不同的年份，而且 *startdate* 和 *enddate* 都在相同的日曆週中，則 **week** 的傳回值將是 0。
  
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
  
## <a name="remarks"></a>Remarks  
DATEDIFF 可用於選取清單、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
DATEDIFF 會以隱含的方式，將字串常值轉換為 **datetime2** 類型。 這表示，將日期當做字串傳遞時，DATEDIFF 不支援 YDM 格式。 您必須明確地將字串轉換為 **datetime** 或 **smalldatetime** 類型，才能使用 YDM 格式。
  
指定 SET DATEFIRST 對 DATEDIFF 沒有任何作用。 DATEDIFF 一定會使用星期天當做一週的第一天，以確保此函數具決定性。
  
## <a name="examples"></a>範例  
下列範例會使用不同的運算式類型，當作 *startdate* 和 *enddate* 參數的引數。
  
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
下列範例會使用使用者定義的變數，當作 *startdate* 和 *enddate* 的引數。
  
```sql
DECLARE @startdate datetime2 = '2007-05-05 12:10:09.3312722';  
DECLARE @enddate datetime2 = '2007-05-04 12:10:09.3312722';   
SELECT DATEDIFF(day, @startdate, @enddate);  
```  
  
### <a name="c-specifying-scalar-system-functions-for-startdate-and-enddate"></a>C. 指定 startdate 和 enddate 的純量系統函數  
下列範例會使用純量系統函數，當作 *startdate* 和 *enddate* 的引數。
  
```sql
SELECT DATEDIFF(millisecond, GETDATE(), SYSDATETIME());  
```  
  
### <a name="d-specifying-scalar-subqueries-and-scalar-functions-for-startdate-and-enddate"></a>D. 指定 startdate 和 enddate 的純量子查詢和純量函數  
下列範例會使用純量子查詢和純量函數，當作 *startdate* 和 *enddate* 的引數。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DATEDIFF(day,(SELECT MIN(OrderDate) FROM Sales.SalesOrderHeader),  
    (SELECT MAX(OrderDate) FROM Sales.SalesOrderHeader));  
```  
  
### <a name="e-specifying-constants-for-startdate-and-enddate"></a>E. 指定 startdate 和 enddate 的常數  
下列範例會使用字元常數，當作 *startdate* 和 *enddate* 的引數。
  
```sql
SELECT DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635');  
```  
  
### <a name="f-specifying-numeric-expressions-and-scalar-system-functions-for-enddate"></a>F. 指定 enddate 的數值運算式和純量系統函數  
下列範例會使用數值運算式 `(GETDATE ()+ 1)` 和純量系統函數 `GETDATE` 與 `SYSDATETIME`，當作 *enddate* 的引數。
  
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
下列範例會使用排名函數，當作 *startdate* 的引數。
  
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
下列範例會使用彙總區間函式，當作 *startdate* 的引數。
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
下列範例會使用不同的運算式類型，當作 *startdate* 和 *enddate* 參數的引數。
  
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
下列範例會使用純量子查詢和純量函數，當作 *startdate* 和 *enddate* 的引數。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day,(SELECT MIN(HireDate) FROM dbo.DimEmployee),  
    (SELECT MAX(HireDate) FROM dbo.DimEmployee))   
FROM dbo.DimEmployee;  
  
```  
  
### <a name="k-specifying-constants-for-startdate-and-enddate"></a>K. 指定 startdate 和 enddate 的常數  
下列範例會使用字元常數，當作 *startdate* 和 *enddate* 的引數。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEDIFF(day, '2007-05-07 09:53:01.0376635'  
    , '2007-05-08 09:53:01.0376635') FROM DimCustomer;  
```  
  
### <a name="l-specifying-ranking-functions-for-startdate"></a>L. 指定 startdate 的排名函數  
下列範例會使用排名函數，當作 *startdate* 的引數。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
,DATEDIFF(day,ROW_NUMBER() OVER (ORDER BY   
        DepartmentName),SYSDATETIME()) AS RowNumber  
FROM dbo.DimEmployee;  
```  
  
### <a name="m-specifying-an-aggregate-window-function-for-startdate"></a>M. 指定 startdate 的彙總視窗函數  
下列範例會使用彙總區間函式，當作 *startdate* 的引數。
  
```sql
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, DepartmentName  
    ,DATEDIFF(year,MAX(HireDate)  
             OVER (PARTITION BY DepartmentName),SYSDATETIME()) AS SomeValue  
FROM dbo.DimEmployee  
```  
  
## <a name="see-also"></a>另請參閱
[DATEDIFF_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-big-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


