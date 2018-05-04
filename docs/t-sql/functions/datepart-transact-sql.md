---
title: DATEPART (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEPART_TSQL
- DATEPART
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], DATEPART
- dateparts [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dateparts [SQL Server], datepart
- comparing dates times [SQL Server]
- DATEPART function [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 15f1a5bc-4c0c-4c48-848d-8ec03473e6c1
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: af3b28322a1d0080202cfc42c3381f8d82d0f535
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回整數，代表指定 *date* 的指定 *datepart*。
  
如需所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函數的概觀，請參閱[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>引數  
*datepart*  
這是會傳回 **integer** 的 *date* 部分 (日期或時間值)。 下表列出所有有效的 *datepart* 引數。 使用者自訂變數對等項目無效。
  
|*datepart*|縮寫|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**、**isoww**|  
  
*date*  
這是可解析成 **time**、**date**、**smalldatetime**、**datetime**、**datetime2** 或 **datetimeoffset** 值的運算式。 *date* 可以是運算式、資料行運算式、使用者定義變數或字串常值。  
若要避免模糊不清，請使用四位數年份。 如需兩位數年份的詳細資訊，請參閱[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
每個 *datepart* 及其縮寫都會傳回相同的值。
  
傳回值會取決於使用 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 及登入的[設定 default language 伺服器組態選項](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)而設定的語言環境，而有所不同。 如果 *date* 是某些格式的字串常值，則傳回值會以使用 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) 所指定的格式為依據。 當 date 是日期或時間資料類型的資料行運算式時，SET DATEFORMAT 並不會影響傳回值。
  
下表針對陳述式 `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')` 列出所有 *datepart* 引數和對應的傳回值。 *date* 引數的資料類型是 **datetimeoffset(7)**。 **nanosecond***datepart* 傳回值具有 9 位數的小數位數 (.123456700)，而且最後兩個位數一定是 00。
  
|*datepart*|傳回值|  
|---|---|
|**year、yyyy、yy**|2007|  
|**quarter、qq、q**|4|  
|**month、mm、m**|10|  
|**dayofyear、dy、y**|303|  
|**day、dd、d**|30|  
|**week、wk、ww**|45|  
|**weekday、dw**|@shouldalert|  
|**hour、hh**|12|  
|**minute、n**|15|  
|**second、ss、s**|32|  
|**millisecond、ms**|123|  
|**microsecond、mcs**|123456|  
|**nanosecond、ns**|123456700|  
|**TZoffset、tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Week 和 weekday datepart 引數
當 *datepart* 是 **week** (**wk**、**ww**) 或 **weekday** (**dw**) 時，傳回值就會取決於使用 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) 所設定的值。
  
任何一年的 1 月 1 日都定義 **week***datepart* 的起始數字，例如：DATEPART (** wk**, 'Jan 1, *xxx*x') = 1，其中 *xxxx* 是任何一年。
  
下表針對每個 SET DATEFIRST 引數的 '2007-04-21'，列出 **week** 和 **weekday***datepart* 的傳回值。 2007 年的 1 月 1 日是星期一。 2007 年的 4 月 21 日是星期六。 SET DATEFIRST 7 (星期日) 是美國的預設值。英國)」。
  
|SET DATEFIRST<br /><br /> 引數 (argument)|week<br /><br /> 傳回|weekday<br /><br /> 傳回|  
|---|---|---|
|@shouldalert|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|@shouldalert|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>year、month 和 day datepart 引數  
針對 DATEPART (**year**、*date*)、DATEPART (**month**、*date*) 和 DATEPART (**day**、*date*) 所傳回的值分別與 [YEAR](../../t-sql/functions/year-transact-sql.md)、[MONTH](../../t-sql/functions/month-transact-sql.md) 和 [DAY](../../t-sql/functions/day-transact-sql.md) 函數傳回的值相同。
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 包含 ISO 週-日期系統 (週數的編號系統)。 每一週都與星期四所在的年份相關聯。 例如，2004 年第 1 週 (2004W01) 從 2003 年 12 月 29 日星期一到 2004 年 1 月 4 日星期日結束。 某個年份的最大週數可能是 52 或 53。 這種編號樣式通常用於歐洲國家/地區，其他國家/地區很少用。
  
不同國家/地區的編號系統可能不會符合 ISO 標準。 目前至少有六種可能，如下表所示。
  
|每週的第一天|一年第一週包含|週指派兩次|使用於|  
|---|---|---|---|
|星期日|1 月 1 日，<br /><br /> 第一個星期六，<br /><br /> 一年的第 1–7 天|是|United States|  
|星期一|1 月 1 日，<br /><br /> 第一個星期日，<br /><br /> 一年的第 1–7 天|是|大部分歐洲國家 (地區) 和英國|  
|星期一|1 月 4 日，<br /><br /> 第一個星期四，<br /><br /> 一年的第 4–7 天|否|ISO 8601、挪威和瑞典|  
|星期一|1 月 7 日，<br /><br /> 第一個星期一，<br /><br /> 一年的第 7 天|否||  
|星期三|1 月 1 日，<br /><br /> 第一個星期二，<br /><br /> 一年的第 1–7 天|是||  
|星期六|1 月 1 日，<br /><br /> 第一個星期五，<br /><br /> 一年的第 1–7 天|是||  
  
## <a name="tzoffset"></a>TZoffset  
**TZoffset** (**tz**) 會以分鐘數傳回 (帶正負號)。 下列陳述式會傳回 310 分鐘的時區位移。
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
TZoffset 值的轉譯方式如下：
- 若是 datetimeoffset 和 datetime2，TZoffset 傳回的時間位移會以分鐘為單位，而 datetime2 的位移一律是 0 分鐘。
- 若是可以隱含轉換成 datetimeoffset 或 datetime2 的資料類型，除了其他日期/時間資料類型之外，會以分鐘為單位傳回時間位移。
- 所有其他類型的參數都會導致錯誤。
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 引數  
當 *date* 是 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 時，秒數就會傳回成 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>針對不在 date 引數中的 datepart 所傳回的預設值  
如果 *date* 引數的資料類型沒有指定的 *datepart*，必須為 *date* 指定一個常值，才會傳回該 *datepart* 的預設值。
  
例如，任何 **date** 資料類型的預設年-月-日都是 1900-01-01。 下列陳述式具有 *datepart* 的日期部分引數、*date* 的時間引數，而且會傳回 `1900, 1, 1, 1, 2`。
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
如果 *date* 指定為變數或資料行，而該變數或資料行的資料類型沒有指定的 *datepart*，則會傳回錯誤 9810。 下列程式碼範例失敗，因為 **time** 資料類型的日期部分年度無效，此資料類型是為變數 *@t* 而宣告。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>小數秒數
下列陳述式會傳回小數秒數：
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Remarks  
DATEPART 可用於選取清單、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，DATEPART 會隱含地將字串常值轉換為 **datetime2** 類型。 這表示，將日期當做字串傳遞時，DATEPART 不支援 YDM 格式。 您必須明確地將字串轉換為 **datetime** 或 **smalldatetime** 類型，才能使用 YDM 格式。
  
## <a name="examples"></a>範例  
下列範例會傳回基底年份。 基底年份可用於日期計算。 在此範例中，日期會指定為數字。 請注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 0 解譯為 1900 年 1 月 1 日。
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
下列範例會傳回日期 `12/20/1974` 的日期部分。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
下列範例會傳回日期 `12/20/1974` 的年份部分。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
1974
```  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
