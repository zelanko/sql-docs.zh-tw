---
title: "DATEPART (TRANSACT-SQL) |Microsoft 文件"
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 05547f2dd50d7f130438d6a07b6952b8c29ec816
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回一個整數，代表指定*datepart*指定*日期*。
  
如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>引數  
*日期部份*  
是的一部分*日期*（日期或時間值） 的**整數**會傳回。 下表列出所有有效*datepart*引數。 使用者自訂變數對等項目無效。
  
|*日期部份*|縮寫|  
|---|---|
|**年份**|**yy**， **yyyy**|  
|**季**|**qq**， **q**|  
|**月份**|**mm**， **m**|  
|**dayofyear**|**dy**， **y**|  
|**一天**|**dd**， **d**|  
|**週**|**wk**， **ww**|  
|**週間日**|**dw**|  
|**小時**|**hh**|  
|**分鐘**|**mi、 n**|  
|**第二個**|**ss**， **s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**奈秒**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**， **isoww**|  
  
*date*  
運算式是可解析成**時間**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是運算式、 資料行運算式、 使用者定義的變數或字串常值。  
若要避免模糊不清，請使用四位數年份。 兩位數年份的相關資訊，請參閱[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>傳回類型  
 **int**  
  
## <a name="return-value"></a>傳回值  
每個*datepart*及其縮寫都會傳回相同的值。
  
傳回的值取決於設定使用的語言環境[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和[設定 default language 伺服器組態選項](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)登入。 如果*日期*是字串常值中，有些格式，傳回的值取決於使用指定的格式[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)。 當 date 是日期或時間資料類型的資料行運算式時，SET DATEFORMAT 並不會影響傳回值。
  
下表列出所有*datepart*具有對應的引數傳回陳述式的值`SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`。 資料型別*日期*引數是**datetimeoffset(7)**。 **奈秒***datepart*傳回值具有小數位數 9 (。 123456700) 而且最後兩個位置一定是 00。
  
|*日期部份*|傳回值|  
|---|---|
|**yy，yyyy，year**|2007|  
|**季、 qq、 q**|4|  
|**月份、 mm、 m**|10|  
|**dayofyear，dy，y**|303|  
|**一天、 dd、 d**|30|  
|**每週、 wk、 ww**|45|  
|**dw 的星期**|1|  
|**小時 hh**|12|  
|**分鐘、 n**|15|  
|**第二個、 ss、 s**|32|  
|**毫秒 ms**|123|  
|**微秒 mcs**|123456|  
|**奈秒 ns**|123456700|  
|**TZoffset tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Week 和 weekday datepart 引數
當*datepart*是**週**(**wk**， **ww**) 或**工作日**(**dw**)，傳回的值取決於使用的設定值[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)。
  
任何一年的 1 年 1 月定義起始數字**週***datepart*，例如： DATEPART (**wk**，' Jan 1， *xxx*x') = 1，其中*xxxx*是任何一年。
  
下表列出的傳回值**週**和**工作日***datepart* ' 2007年-04-21' 每個 SET DATEFIRST 引數。 2007 年的 1 月 1 日是星期一。 2007 年的 4 月 21 日是星期六。 SET DATEFIRST 7 (星期日) 是美國的預設值。英國)」。
  
|SET DATEFIRST<br /><br /> 引數 (argument)|week<br /><br /> 傳回|weekday<br /><br /> 傳回|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>year、month 和 day datepart 引數  
針對 DATEPART 所傳回的值 (**年**，*日期*)，DATEPART (**月份**，*日期*)，和 DATEPART (**一天**，*日期*) 所傳回的函式相同[年](../../t-sql/functions/year-transact-sql.md)，[月份](../../t-sql/functions/month-transact-sql.md)，和[天](../../t-sql/functions/day-transact-sql.md)，f分別。
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 包含 ISO 週-日期系統 (週數的編號系統)。 每一週都與星期四所在的年份相關聯。 例如，2004 年第 1 週 (2004W01) 從 2003 年 12 月 29 日星期一到 2004 年 1 月 4 日星期日結束。 某個年份的最大週數可能是 52 或 53。 這種編號樣式通常用於歐洲國家/地區，其他國家/地區很少用。
  
不同國家/地區的編號系統可能不會符合 ISO 標準。 目前至少有六種可能，如下表所示。
  
|每週的第一天|一年第一週包含|週指派兩次|使用於|  
|---|---|---|---|
|星期日|1 月 1 日，<br /><br /> 第一個星期六，<br /><br /> 一年的第 1–7 天|是|United States|  
|星期一|1 月 1 日，<br /><br /> 第一個星期日，<br /><br /> 一年的第 1–7 天|是|大部分歐洲國家 (地區) 和英國|  
|星期一|4 年 1 月，<br /><br /> 第一個星期四，<br /><br /> 一年的 4-7 天|否|ISO 8601、挪威和瑞典|  
|星期一|7 月，<br /><br /> 第一個星期一，<br /><br /> 一年的第 7 天|否||  
|星期三|1 月 1 日，<br /><br /> 第一個星期二，<br /><br /> 一年的第 1–7 天|是||  
|星期六|1 月 1 日，<br /><br /> 第一個星期五，<br /><br /> 一年的第 1–7 天|是||  
  
## <a name="tzoffset"></a>TZoffset  
**TZoffset** (**tz**) 會當成 （帶正負號） 的分鐘數。 下列陳述式會傳回 310 分鐘的時區位移。
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
TZoffset 值轉譯，如下所示：
- Datetimeoffset 和 datetime2，TZoffset 傳回的時間位移以分鐘為單位的位移 datetime2 是一律從 0 分鐘。
- 資料類型可以隱含地轉換成 datetimeoffset 或 datetime2，除了其他日期/時間資料類型，它會以分鐘為單位傳回時間位移。
- 所有其他類型的參數會導致錯誤。
  
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 引數  
當*日期*是[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)，秒就會傳回成 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>針對不在 date 引數中的 datepart 所傳回的預設值  
資料類型，是否*日期*引數並沒有指定*datepart*，該預設*datepart* 指定常值時，才會傳回*日期*。
  
例如，預設年-月-日任何**日期**資料類型是 1900年-01-01。 下列陳述式都有的日期部分引數*datepart*，時間引數的*日期*，並傳回`1900, 1, 1, 1, 2`。
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
如果*日期*指定為變數或資料表資料行和資料類型的變數或資料行沒有指定*datepart*，會傳回錯誤 9810。 下列程式碼範例失敗，因為不是有效的日期部分年度**時間**宣告變數的資料型別 *@t* 。
  
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
  
## <a name="remarks"></a>備註  
DATEPART 可用於選取清單、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，DATEPART 會隱含地將轉換為字串常值**datetime2**型別。 這表示，將日期當做字串傳遞時，DATEPART 不支援 YDM 格式。 您必須明確地將字串轉換成**datetime**或**smalldatetime**類型才能使用 YDM 格式。
  
## <a name="examples"></a>範例  
下列範例會傳回基底年份。 基底年份可用於日期計算。 在此範例中，日期會指定為數字。 請注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將 0 解譯為 1900 年 1 月 1 日。
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
下列範例會傳回日期的日期部分`12/20/1974`。
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
下列範例會傳回日期的年份部分`12/20/1974`。
  
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
  
  

