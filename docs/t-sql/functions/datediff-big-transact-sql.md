---
title: "DATEDIFF_BIG (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 7
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 08f27953aac5fa36f1b38e243d8465f57458dafe
ms.contentlocale: zh-tw
ms.lasthandoff: 10/12/2017

---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

傳回指定的計數 （帶正負號的大整數） *datepart*界限跨越指定*startdate*和*enddate*。
  
如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
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
 已簽署   
        **bigint**  
  
## <a name="return-value"></a>傳回值  
傳回在指定日期部分界限的計數 (帶正負號的 bigint) 跨越指定的 startdate 和 enddate。
-   每個*datepart*及其縮寫都會傳回相同的值。  
  
如果傳回的值超出範圍**bigint** (是-9223372036854775808 到 9,223,372,036,854,775,807)，則會傳回錯誤。 如**毫秒**，之間的最大差異*startdate*和*enddate*是 24 天、 20 小時 31 分鐘和 23.647 秒。 如**第二個**，最大的差異是 68 年。
  
如果*startdate*和*enddate*同時指派時間值和*datepart*不是時間*datepart*，就會傳回 0。
  
時區位移元件*startdate*或*endate*不會用於計算傳回的值。
  
因為[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)的精確度只有到分鐘，當**smalldatetime**值用於*startdate*或*enddate*、 秒和毫秒為單位永遠會設定為 0 的傳回值。
  
如果只將時間值指派給日期資料類型的變數，則遺漏日期部分的值設定為預設值： 1900年-01-01。 如果只是日期值指派給時間或日期的資料類型的變數，遺漏時間部分的值會設定為預設值： 00:00:00。 如果有任一個*startdate*或*enddate*只有時間部分和其他只有日期部分、 遺漏的時間和日期部分設定為預設值。
  
如果*startdate*和*enddate*是不同的日期資料類型，另一個有更多的時間部分或小數秒數有效位數超過另，其他遺失的組件會設定為 0。
  
## <a name="datepart-boundaries"></a>datepart 界限
下列陳述式具有相同*startdate*和相同*endate*。 這些日期都很接近而且時間差距為 .0000001 秒。 之間的差異*startdate*和*endate*每個陳述式中已超過一個日曆或時間界限的其*datepart*。 每個陳述式都會傳回 1。 如果這個範例會使用不同的年份，如果兩個*startdate*和*endate*位於相同的日曆週的傳回值**週**就是 0。

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
  
## <a name="remarks"></a>備註  
DATEDIFF_BIG 可用於選取清單、 WHERE、 HAVING、 GROUP BY 和 ORDER BY 子句。
  
DATEDIFF_BIG 隱含地將轉換為字串常值**datetime2**型別。 這表示，DATEDIFF_BIG 不支援 YDM 格式將日期當做字串傳遞時。 您必須明確地將字串轉換成**datetime**或**smalldatetime**類型才能使用 YDM 格式。
  
指定 SET DATEFIRST DATEDIFF_BIG 沒有作用。 DATEDIFF_BIG 一律使用星期天當做一週的第一天，以確保此函數具決定性。
  
## <a name="examples"></a>範例  
下列範例會使用不同類型的運算式做為引數*startdate*和*enddate*參數。
  
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
  
許多其他範例，請參閱中緊密相關的範例[DATEDIFF &#40;TRANSACT-SQL &#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;TRANSACT-SQL &#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  

