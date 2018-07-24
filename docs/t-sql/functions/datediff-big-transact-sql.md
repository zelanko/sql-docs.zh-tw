---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b309bb7411d3c75aa1c98a219123efffc5dbca3e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38063616"
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

此函式會傳回跨越指定之 *startdate* 和 *enddate* 的指定之 *datepart* 界限的計數 (作為帶正負號的大整數值)。
  
如需所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函式的概觀，請參閱[日期和時間資料類型與函式 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>引數  
*datepart*  
指定所跨越界限類型之 *startdate* 和 *enddate* 的一部分。 `DATEDIFF_BIG` 不會接受使用者定義變數對等項目。 此表格會列出所有有效的 *datepart* 引數。

> [!NOTE]
> `DATEDIFF_BIG` 不會接受 *datepart* 引數的使用者定義變數對等項目。
  
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
可解析成下列其中一個值的運算式：

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

針對 *date*，`DATEDIFF_BIG` 會接受資料行運算式、運算式、字串常值或使用者定義變數。 字串常值必須解析成 **datetime**。 請使用四位數年份以避免模糊不清的問題。 `DATEDIFF_BIG` 會從 *startdate* 減去 *enddate*。 若要避免模糊不清，請使用四位數年份。 如需兩位數年份的資訊，請參閱[設定兩位數年份的截止伺服器設定選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
*enddate*  
請參閱＜*startdate*＞。
  
## <a name="return-type"></a>傳回類型  

帶正負號的 **bigint**  
  
## <a name="return-value"></a>傳回值  
傳回跨越指定 startdate 和 enddate 之指定 datepart 界限的計數 (作為帶正負號的 Bigint 值)。
-   每個特定 *datepart* 和該 *datepart* 的縮寫會傳回相同的值。  
  
針對超出 **bigint** 範圍 (-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807) 的傳回值，`DATEDIFF_BIG` 會傳回錯誤。 針對 **millisecond**，*startdate* 和 *enddate* 最大的差異為 24 天 20 小時 31 分鐘 23.647 秒。 針對 **second**，最大的差異為 68 年。
  
如果 *startdate* 和 *enddate* 都只獲指派時間值，且 *datepart* 不是時間 *datepart*，`DATEDIFF_BIG` 會傳回 0。
  
`DATEDIFF_BIG` 不會使用 *startdate* 或 *enddate* 的時區時差元件來計算傳回值。
  
針對用於 *startdate* 或 *enddate* 的 **smalldatetime** 值，`DATEDIFF_BIG` 一律會在傳回值中將秒和毫秒設定為 0，因為 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 的精確度只有到分鐘。
  
如果您只有將時間值指派給日期資料類型變數，`DATEDIFF_BIG` 會將遺漏日期部分的值設定為預設值：1900-01-01。 如果您只有將日期值指派給時間或日期資料類型的變數，`DATEDIFF_BIG` 會將遺漏時間部分的值設定為預設值：00:00:00。 如果 *startdate* 或 *enddate* 其中之一只有時間部分，而另一個只有日期部分，`DATEDIFF_BIG` 會將遺漏的時間和日期部分設定為預設值。
  
如果 *startdate* 和 *enddate* 具有不同的日期資料類型，而且其中一個項目的時間部分或小數秒數有效位數超過另一個項目，`DATEDIFF_BIG` 會將另一個項目的遺漏部分設定為 0。
  
## <a name="datepart-boundaries"></a>datepart 界限
下列陳述式具有相同的 *startdate* 和相同的 *enddate* 值。 這些日期都很接近而且時間差距為 .0000001 秒。 每個陳述式中 *startdate* 與 *enddate* 之間的差異會跨越其 *datepart* 的日曆或時間界限。 每個陳述式都會傳回 1。 如果 *startdate* 和 *enddate* 具有不同的年份值，但具有相同的日曆週值，`DATEDIFF_BIG` 會針對 *datepart* **week** 傳回 0。

```sql
SELECT DATEDIFF_BIG(year,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter,     '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month,       '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear,   '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day,         '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour,        '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second,      '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
您可以在 SELECT <list>、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中使用 `DATEDIFF_BIG`。
  
`DATEDIFF_BIG` 會以隱含的方式，將字串常值轉換為 **datetime2** 類型。 這表示，將日期當作字串傳遞時，`DATEDIFF_BIG` 不支援 YDM 格式。 您必須明確地將字串轉換為 **datetime** 或 **smalldatetime** 類型，才能使用 YDM 格式。
  
指定 SET DATEFIRST 對 `DATEDIFF_BIG` 沒有任何作用。 `DATEDIFF_BIG` 一律會使用星期天當作一週的第一天，以確保此函式以具決定性的方式運作。
  
## <a name="examples"></a>範例 
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>指定 startdate 和 enddate 的資料行  
此範例會使用不同的運算式類型，當作 *startdate* 和 *enddate* 參數的引數。 它會計算資料表的兩個資料行之間的日期已跨越的天數界限。
  
```sql
CREATE TABLE dbo.Duration  
    (startDate datetime2, endDate datetime2);  
    
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09', '2007-05-07 12:10:09');  
    
SELECT DATEDIFF_BIG(day, startDate, endDate) AS 'Duration'  
    FROM dbo.Duration;  
-- Returns: 1  
```  

請參閱 [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md) 中更緊密相關的範例。
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
