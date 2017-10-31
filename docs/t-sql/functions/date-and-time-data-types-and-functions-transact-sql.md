---
title: "日期和時間資料類型與函數 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
caps.latest.revision: 79
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 7ce3baac7ec87ff3cad771234ab1196fb0a3855e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/06/2017

---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>日期和時間資料類型與函數 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

本主題中的下列各節會提供所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間資料類型與函數的概觀。
-   [日期和時間資料類型](#DateandTimeDataTypes)  
-   [日期和時間函數](#DateandTimeFunctions)  
    -   [取得系統日期和時間值的函式](#GetSystemDateandTimeValues)  
    -   [函數可取得日期和時間部分](#GetDateandTimeParts)  
    -   [從各自部分取得日期和時間值的函式](#fromParts)  
    -   [函數可取得日期和時間差異](#GetDateandTimeDifference)  
    -   [函式，修改日期和時間值](#ModifyDateandTimeValues)  
    -   [設定或取得工作階段格式函式的函式](#SetorGetSessionFormatFunctions)  
    -   [函式會驗證日期和時間值](#ValidateDateandTimeValues)  
-   [日期和時間相關的主題](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a>日期和時間資料類型
[!INCLUDE[tsql](../../includes/tsql-md.md)]日期和時間資料類型會列在下表：
  
|資料類型|格式|範圍|精確度|儲存體大小 (位元組)|使用者自訂的小數秒數有效位數|時區位移|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|00:00:00.0000000 到 23:59:59.9999999|100 奈秒|3 到 5|是|否|  
|[date](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|0001-01-01 到 31.12.99|1 日|3|否|否|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss|1900-01-01 到 2079-06-06|1 分鐘|4|否|否|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnn]|1753-01-01 到 9999-12-31|0.00333 秒鐘|8|否|否|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|0001-01-01 00:00:00.0000000 到 9999-12-31 23:59:59.9999999|100 奈秒|6 到 8|是|否|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|0001-01-01 00:00:00.0000000 到 9999-12-31 23:59:59.9999999 (以 UTC 為單位)|100 奈秒|8 到 10|是|是|  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../includes/tsql-md.md)] [Rowversion](../../t-sql/data-types/rowversion-transact-sql.md)資料類型不是日期或時間資料型別。 **時間戳記**是已被取代的同義字**rowversion**。  
  
##  <a name="DateandTimeFunctions"></a>日期和時間函數  
[!INCLUDE[tsql](../../includes/tsql-md.md)] 日期和時間函數會列在下表中。 如需決定性的詳細資訊，請參閱[決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。
  
###  <a name="GetSystemDateandTimeValues"></a>取得系統日期和時間值的函式 
所有系統日期和時間值都是衍生自執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的作業系統。
  
#### <a name="higher-precision-system-date-and-time-functions"></a>較高精確度的系統日期和時間函數  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]使用 GetSystemTimeAsFileTime() Windows API 來取得日期和時間值。 精確度取決於執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦硬體和 Windows 版本。 此 API 的精確度是固定於 100 奈秒。 使用 GetSystemTimeAdjustment() Windows API，可判斷精確度。
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|傳回**datetime2 （7)**值，其中包含的日期和時間的電腦上的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 時區位移並不包括在內。|**datetime2(7)**|不具決定性|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|傳回**datetimeoffset(7)**值，其中包含的日期和時間的電腦上的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 時區位移包括在內。|**datetimeoffset(7)**|不具決定性|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|傳回**datetime2 （7)**值，其中包含的日期和時間的電腦上的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 以 UTC 時間 （國際標準時間） 傳回的日期和時間。|**datetime2(7)**|不具決定性|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>較低精確度的系統日期和時間函數
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|傳回**datetime**值，其中包含的日期和時間的電腦上的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 時區位移並不包括在內。|**datetime**|不具決定性|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|傳回**datetime**值，其中包含的日期和時間的電腦上的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 時區位移並不包括在內。|**datetime**|不具決定性|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|傳回**datetime**值，其中包含的日期和時間的電腦上的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行。 以 UTC 時間 （國際標準時間） 傳回的日期和時間。|**datetime**|不具決定性|  
  
###  <a name="GetDateandTimeParts"></a>取得日期和時間部分的函式
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* ，*日期*)|傳回代表指定之字元字串*datepart*的指定日期。|**nvarchar**|不具決定性|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* ，*日期*)|傳回一個整數，代表指定*datepart*指定*日期*。|**int**|不具決定性|  
|[一天](../../t-sql/functions/day-transact-sql.md)|日 (*日期*)|傳回一個整數，表示指定的日期部分*日期*。|**int**|具決定性|  
|[月份](../../t-sql/functions/month-transact-sql.md)|月 (*日期*)|傳回一個整數，表示指定的月份部分*日期*。|**int**|具決定性|  
|[年份](../../t-sql/functions/year-transact-sql.md)|年份 (*日期*)|傳回一個整數，表示指定的年部分*日期*。|**int**|具決定性|  
  
###  <a name="fromParts"></a>從各自部分取得日期和時間值的函式
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS (*年*，*月份*，*天*)|傳回**日期**指定的年、 月和日的值。|**date**|具決定性|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS (*年*，*月份*，*天*，*小時*，*分鐘*，*秒*，*分數*，*精確度*)|傳回**datetime2**具有指定的有效位數及指定的日期和時間值。|**datetime2 (** *精確度* **)**|具決定性|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS (*年*，*月份*，*天*，*小時*，*分鐘*，*秒*，*毫秒*)|傳回**datetime**指定的日期和時間值。|**datetime**|具決定性|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS (*年*，*月份*，*天*，*小時*，*分鐘*， *秒*，*分數*， *hour_offset*， *minute_offset*，*精確度*)|傳回**datetimeoffset**具有指定的時差和精確度及指定的日期和時間值。|**datetime (** *精確度* **)**|具決定性|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS (*年*，*月份*，*天*，*小時*，*分鐘*)|傳回**smalldatetime**指定的日期和時間值。|**smalldatetime**|具決定性|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS (*小時*，*分鐘*，*秒*，*分數*，*精確度*)|傳回**時間**針對指定的時間並使用指定的有效位數的值。|**時間 (** *精確度* **)**|具決定性|  
  
###  <a name="GetDateandTimeDifference"></a>取得日期和時間差異的函式
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* ， *startdate* ， *enddate* )|傳回日期或時間的數目*datepart*會跨越兩個指定日期的界限。|**int**|具決定性|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* ， *startdate* ， *enddate* )|傳回日期或時間的數目*datepart*會跨越兩個指定日期的界限。|**bigint**|具決定性|  
  
###  <a name="ModifyDateandTimeValues"></a>修改日期和時間值的函式
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* ，*數目*，*日期*)|傳回新**datetime**根據將間隔加入指定的值*datepart*指定*日期*。|資料型別*日期*引數|具決定性|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH ( *start_date* [，*具有 month_to_add* ])|以選擇性位移，傳回包含指定日期的當月最後一天。|傳回類型是*start_date*或**日期**。|具決定性|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|交換器*位移*(*DATETIMEOFFSET* ， *time_zone*)|交換器*位移*變更時區時差的 DATETIMEOFFSET 值，並保留 UTC 值。|**datetimeoffset**的小數有效位數與*DATETIMEOFFSET*|具決定性|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*運算式*， *time_zone*)|TODATETIMEOFFSET 會將 datetime2 值轉換成 datetimeoffset 值。 datetime2 值會針對指定的 time_zone 以當地時間解譯。|**datetimeoffset**的小數有效位數與*datetime*引數|具決定性|  
  
###  <a name="SetorGetSessionFormatFunctions"></a>取得或設定工作階段格式的函式
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|傳回 SET DATEFIRST 之工作階段的目前值。|**tinyint**|不具決定性|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST {*數目*&#124; **@**  *number_var* }|將一週的第一天設為 1-7 其中一個數字。|不適用|不適用|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT {*格式*&#124; **@**  *format_var* }|輸入設定的日期部分 （月/日/年） 順序**datetime**或**smalldatetime**資料。|不適用|不適用|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|傳回目前所用語言的名稱。 @@LANGUAGE不是日期或時間的函式。 不過，語言設定可能會影響日期函數的輸出。|不適用|不適用|  
|[設定語言](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE {[N] **'***語言***'** &#124; **@**  *language_var* }|設定工作階段和系統訊息的語言環境。 SET LANGUAGE 不是日期或時間函數。 不過，語言設定會影響日期函數的輸出。|不適用|不適用|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [[  **@language =** ] **'***語言***'** ]|傳回所有支援語言之日期格式的詳細資訊。 **sp_helplanguage**不是日期或時間預存程序。 不過，語言設定會影響日期函數的輸出。|不適用|不適用|  
  
###  <a name="ValidateDateandTimeValues"></a>驗證日期和時間值的函式
  
|函數|語法|傳回值|傳回資料類型|決定性|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE (*運算式*)|決定是否**datetime**或**smalldatetime**輸入的運算式是有效的日期或時間值。|**int**|只有在搭配 CONVERT 函數使用、已指定 CONVERT 樣式參數，而且樣式不等於 0、100、9 或 109 時，ISDATE 才具有決定性。|  
  
##  <a name="DateandTimeRelatedTopics"></a>日期和時間相關的主題 
  
|主題|Description|  
|-----------|-----------------|  
|[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|提供將日期和時間值在字串常值與其他日期和時間格式之間來回轉換的相關資訊。|  
|[撰寫國際通用的 Transact-SQL 陳述式](../../relational-databases/collations/write-international-transact-sql-statements.md)|提供的指導方針可攜性的資料庫和資料庫應用程式使用[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式從一種語言到另一個，或可支援多種語言。|  
|[ODBC 純量函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|提供可用於 ODBC 純量函數的相關資訊[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。 這包括 ODBC 日期和時間函數。|  
|[TIME ZONE &AMP; #40;TRANSACT-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|提供時區轉換。|  
  
## <a name="see-also"></a>另請參閱
[函數](../../t-sql/functions/functions.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

