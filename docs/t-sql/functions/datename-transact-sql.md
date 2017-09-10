---
title: "DATENAME (TRANSACT-SQL) |Microsoft 文件"
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
- DATENAME_TSQL
- DATENAME
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATENAME function [SQL Server
- functions [SQL Server], time
- functions [SQL Server], date and time
- dateparts [SQL Server], datename
- date and time [SQL Server], DATENAME
- comparing dates times [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 11855b56-c554-495d-aad4-ba446990153b
caps.latest.revision: 59
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d41bbf5a83f0dee8518ece6f074181b8412bad8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回代表指定之字元字串*datepart*指定*日期*
  
如需所有[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料型別和函式，請參閱[日期和時間資料型別和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>引數  
*日期部份*  
是的一部分*日期*傳回。 下表列出所有有效*datepart*引數。 使用者自訂變數對等項目無效。
  
|*日期部份*|縮寫|  
|---|---|
|**年份**|**yy、 yyyy**|  
|**季**|**qq、 q**|  
|**月份**|**mm、 m**|  
|**dayofyear**|**dy、 y**|  
|**一天**|**dd、 d**|  
|**週**|**wk、 ww**|  
|**週間日**|**dw、 w**|  
|**小時**|**hh**|  
|**分鐘**|**mi、 n**|  
|**第二個**|**ss、 s**|  
|**毫秒**|**ms**|  
|**微秒**|**mcs**|  
|**奈秒**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK ISOWW**|  
  
*date*  
運算式是可解析成**時間**，**日期**， **smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。 *日期*可以是運算式、 資料行運算式、 使用者定義的變數或字串常值。  
若要避免模糊不清，請使用四位數年份。 如需兩位數年份，請參閱[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>傳回類型  
**nvarchar**
  
## <a name="return-value"></a>傳回值  
  
-   每個*datepart*及其縮寫都會傳回相同的值。  
  
傳回的值取決於設定使用的語言環境[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和[設定 default language 伺服器組態選項](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)登入。 傳回值就會相依於[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)如果*日期*是字串常值的某些格式。 當 date 是日期或時間資料類型的資料行運算式時，SET DATEFORMAT 並不會影響傳回值。
  
當*日期*參數具有**日期**資料型別引數，傳回的值取決於所使用指定的設定[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)。
  
## <a name="tzoffset-datepart-argument"></a>TZoffset datepart 引數  
如果*datepart*引數是**TZoffset** (**tz**) 和*日期*引數有沒有時區時差，就會傳回 0。
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 引數  
當*日期*是[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)，秒就會傳回成 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>針對不在 date 引數中的 datepart 所傳回的預設值  
資料類型，是否*日期*引數並沒有指定*datepart*，該預設*datepart* 指定常值時，才會傳回*日期*。
  
例如，預設年-月-日任何**日期**資料類型是 1900年-01-01。 下列陳述式都有的日期部分引數*datepart*，時間引數的*日期*，並傳回`1900, January, 1, 1, Monday`。
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
如果*日期*指定為變數或資料表資料行和資料類型的變數或資料行沒有指定*datepart*，會傳回錯誤 9810。 下列程式碼範例失敗，因為不是有效的日期部分年度**時間**宣告變數的資料型別 *@t* 。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>備註  
DATENAME 可用於選取清單、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，DATENAME 會隱含地將轉換為字串常值**datetime2**型別。 這表示，將日期當做字串傳遞時，DATENAME 不支援 YDM 格式。 您必須明確地將字串轉換成**datetime**或**smalldatetime**類型才能使用 YDM 格式。
  
## <a name="examples"></a>範例  
下列範例會針對指定的日期傳回日期部分。
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*日期部份*|傳回值|  
|---|---|
|**yy，yyyy，year**|2007|  
|**季、 qq、 q**|4|  
|**月份、 mm、 m**|十月|  
|**dayofyear，dy，y**|303|  
|**一天、 dd、 d**|30|  
|**每週、 wk、 ww**|44|  
|**dw 的星期**|星期二|  
|**小時 hh**|12|  
|**分鐘、 n**|15|  
|**第二個、 ss、 s**|32|  
|**毫秒 ms**|123|  
|**微秒 mcs**|123456|  
|**奈秒 ns**|123456700|  
|**TZoffset tz**|310|  
|**ISO_WEEK，ISOWK，ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

下列範例會針對指定的日期傳回日期部分。
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*日期部份*|傳回值|  
|---|---|
|**yy，yyyy，year**|2007|  
|**季、 qq、 q**|4|  
|**月份、 mm、 m**|十月|  
|**dayofyear，dy，y**|303|  
|**一天、 dd、 d**|30|  
|**每週、 wk、 ww**|44|  
|**dw 的星期**|星期二|  
|**小時 hh**|12|  
|**分鐘、 n**|15|  
|**第二個、 ss、 s**|32|  
|**毫秒 ms**|123|  
|**微秒 mcs**|123456|  
|**奈秒 ns**|123456700|  
|**TZoffset tz**|310|  
|**ISO_WEEK，ISOWK，ISOWW**|44|  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


