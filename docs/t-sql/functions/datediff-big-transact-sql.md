---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6c8228f0db3e37fe3bf6425d60fd4f9067e92220
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

傳回跨越指定 *startdate* 和 *enddate* 之 *datepart* 界限的計數 (帶正負號的整數)。
  
如需所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函式的概觀，請參閱[日期和時間資料類型與函式 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>引數  
*datepart*  
這是指定所跨越之界限類型的 *startdate* 和 *enddate* 部分。 下表列出所有有效的 *datepart* 引數。 使用者自訂變數對等項目無效。
  
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
為可解析成 **time**、**date**、**smalldatetime**、**datetime**、**datetime2** 或 **datetimeoffset** 值的運算式。 *date* 可以是運算式、資料行運算式、使用者自訂變數或字串常值。 *startdate* 會從 *enddate* 減去。  
若要避免模糊不清，請使用四位數年份。 如需兩位數年份的詳細資訊，請參閱[設定兩位數年份的截止伺服器設定選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
*enddate*  
請參閱 *startdate*。
  
## <a name="return-type"></a>傳回類型  
 已簽署   
        **bigint**  
  
## <a name="return-value"></a>傳回值  
傳回跨越指定 startdate 與 enddate 之 datepart 界限的計數 (帶正負號的 bigint)。
-   每個 *datepart* 及其縮寫都會傳回相同的值。  
  
若傳回值超出 **bigint** 的範圍 (-9,223,372,036,854,775,808 到 9,223,372,036,854,775,807)，便會傳回錯誤。 針對 **millisecond**，*startdate* 和 *enddate* 最大的差異為 24 天 20 小時 31 分鐘及 23.647 秒。 針對 **second**，最大的差異為 68 年。
  
若 *startdate* 和 *enddate* 都只指派時間值，且 *datepart* 不是時間 *datepart*，則會傳回 0。
  
*startdate* 或 *enddate* 的時區位移元件不會用於計算傳回值。
  
由於 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 的精確度只有到分鐘，因此當 **smalldatetime** 值用於 *startdate* 或 *enddate* 時，秒和毫秒就一律會在傳回值中設定為 0。
  
如果您只有將時間值指派給日期資料類型的變數，則遺漏日期部分的值就會設定為預設值：1900-01-01。 如果您只有將日期值指派給時間或日期資料類型的變數，則遺漏時間部分的值就會設定為預設值：00:00:00。 若 *startdate* 或 *enddate* 其中之一只有時間部分，而且另一個項目只有日期部分，則遺漏的時間和日期部分都會設定為預設值。
  
如果 *startdate* 和 *enddate* 具有不同的日期資料類型，而且其中一個項目的時間部分或小數秒數有效位數超過另一個項目，則另一個項目的遺漏部分就會設定為 0。
  
## <a name="datepart-boundaries"></a>datepart 界限
下列陳述式具有相同的 *startdate* 和相同的 *enddate*。 這些日期都很接近而且時間差距為 .0000001 秒。 每個陳述式中 *startdate* 與 *enddate* 之間的差異會跨越其 *datepart* 的日曆或時間界限。 每個陳述式都會傳回 1。 如果這個範例使用不同的年份，而且 *startdate* 和 *enddate* 都在相同的日曆週中，則 **week** 的傳回值就是 0。

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Remarks  
DATEDIFF_BIG 可用於選取清單、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
DATEDIFF_BIG 會隱含的將字串常值轉換為 **datetime2** 類型。 這表示，將日期當作字串傳遞時，DATEDIFF_BIG 不支援 YDM 格式。 您必須明確地將字串轉換為 **datetime** 或 **smalldatetime** 類型，才能使用 YDM 格式。
  
指定 SET DATEFIRST 對 DATEDIFF_BIG 沒有任何作用。 DATEDIFF_BIG 一律會使用星期天當作一週的第一天，以確保此函式具確定性。
  
## <a name="examples"></a>範例  
下列範例會使用不同的運算式類型，當作 *startdate* 和 *enddate* 參數的引數。
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>指定 startdate 和 enddate 的資料行  
下列範例會計算資料表中兩個資料行之間的日期已跨越的天數界限。
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
如需許多其他範例，請參閱 [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md) 中密切相關的範例。
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
