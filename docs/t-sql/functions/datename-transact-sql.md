---
title: DATENAME (Transact-SQL) | Microsoft Docs
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a8803278c567f01888b7b530885e82e4543c966a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回代表指定 *date* 之指定 *datepart* 的字元字串
  
如需所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函數的概觀，請參閱[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>引數  
*datepart*  
這是要傳回的 *date* 部分。 下表列出所有有效的 *datepart* 引數。 使用者自訂變數對等項目無效。
  
|*datepart*|縮寫|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**weekday**|**dw, w**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
這是可解析成 **time**、**date**、**smalldatetime**、**datetime**、**datetime2** 或 **datetimeoffset** 值的運算式。 *date* 可以是運算式、資料行運算式、使用者定義變數或字串常值。  
若要避免模糊不清，請使用四位數年份。 如需兩位數年份的資訊，請參閱 [設定兩位數年份的截止伺服器設定選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。
  
## <a name="return-type"></a>傳回類型  
**nvarchar**
  
## <a name="return-value"></a>傳回值  
  
-   每個 *datepart* 及其縮寫都會傳回相同的值。  
  
傳回值會根據使用 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) 所設定的語言環境並依據登入的[設定預設語言伺服器設定選項](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)而不同。 如果 *date* 是某些格式的字串常值，傳回值就會相依於 [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)。 當 date 是日期或時間資料類型的資料行運算式時，SET DATEFORMAT 並不會影響傳回值。
  
當 *date* 參數具有 **date** 資料類型引數時，傳回值就會根據使用 [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md) 所指定的設定而不同。
  
## <a name="tzoffset-datepart-argument"></a>TZoffset datepart 引數  
如果 *datepart* 引數是 **TZoffset** (**tz**) 而且 *date* 引數沒有時區時差，就會傳回 0。
  
## <a name="smalldatetime-date-argument"></a>smalldatetime date 引數  
當 *date* 是 [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) 時，秒數就會傳回成 00。
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>針對不在 date 引數中的 datepart 所傳回的預設值  
如果 *date* 引數的資料類型沒有指定的 *datepart*，必須為 *date* 指定一個常值，才會傳回該 *datepart* 的預設值。
  
例如，任何 **date** 資料類型的預設年-月-日都是 1900-01-01。 下列陳述式具有 *datepart* 的日期部分引數、*date* 的時間引數，而且會傳回 `1900, January, 1, 1, Monday`。
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
如果 *date* 指定為變數或資料行，而該變數或資料行的資料類型沒有指定的 *datepart*，則會傳回錯誤 9810。 下列程式碼範例失敗，因為 **time** 資料類型的日期部分年度無效，此資料類型是為變數 *@t* 而宣告。
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Remarks  
DATENAME 可用於選取清單、WHERE、HAVING、GROUP BY 和 ORDER BY 子句中。
  
在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，DATENAME 會隱含地將字串常值轉換為 **datetime2** 類型。 這表示，將日期當做字串傳遞時，DATENAME 不支援 YDM 格式。 您必須明確地將字串轉換為 **datetime** 或 **smalldatetime** 類型，才能使用 YDM 格式。
  
## <a name="examples"></a>範例  
下列範例會針對指定的日期傳回日期部分。
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|傳回值|  
|---|---|
|**year、yyyy、yy**|2007|  
|**quarter、qq、q**|4|  
|**month、mm、m**|十月|  
|**dayofyear、dy、y**|303|  
|**day、dd、d**|30|  
|**week、wk、ww**|44|  
|**weekday、dw**|星期二|  
|**hour、hh**|12|  
|**minute、n**|15|  
|**second、ss、s**|32|  
|**millisecond、ms**|123|  
|**microsecond、mcs**|123456|  
|**nanosecond、ns**|123456700|  
|**TZoffset、tz**|310|  
|**ISO_WEEK、ISOWK、ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

下列範例會針對指定的日期傳回日期部分。
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|傳回值|  
|---|---|
|**year、yyyy、yy**|2007|  
|**quarter、qq、q**|4|  
|**month、mm、m**|十月|  
|**dayofyear、dy、y**|303|  
|**day、dd、d**|30|  
|**week、wk、ww**|44|  
|**weekday、dw**|星期二|  
|**hour、hh**|12|  
|**minute、n**|15|  
|**second、ss、s**|32|  
|**millisecond、ms**|123|  
|**microsecond、mcs**|123456|  
|**nanosecond、ns**|123456700|  
|**TZoffset、tz**|310|  
|**ISO_WEEK、ISOWK、ISOWW**|44|  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

