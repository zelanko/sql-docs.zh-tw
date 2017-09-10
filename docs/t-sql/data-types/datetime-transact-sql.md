---
title: "datetime (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetime_TSQL
- datetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetime
- dates [SQL Server], data types
- datetime data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: 9bd1cc5b-227b-4032-95d6-7581ddcc9924
caps.latest.revision: 64
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae40eaacd6fd441ce0bdbadd3af02b7b189704a2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datetime-transact-sql"></a>datetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定義日期，並結合了以 24 小時制為基礎的當日時間和小數秒數。
  
> [!NOTE]  
>  使用**時間**，**日期**， **datetime2**和**datetimeoffset**新工作的資料型別。 這些類型符合 SQL 標準。 它們具有方便移植的特性。 **時間**， **datetime2**和**datetimeoffset**提供更多秒數有效位數。 **datetimeoffset**全域部署的應用程式提供時區支援。  
  
## <a name="datetime-description"></a>datetime 描述  
  
|屬性|值|  
|---|---|
|語法|**datetime**|  
|使用方式|宣告@MyDatetime**日期時間**<br /><br /> 建立資料表 Table1 (Column1 **datetime** )|  
|預設的字串常值格式<br /><br /> (用於下層用戶端)|不適用|  
|日期範圍|1753 年 1 月 1 日到 9999 年 12 月 31 日|  
|時間範圍|00:00:00 到 23:59:59.997|  
|時區位移範圍|無|  
|元素範圍|YYYY 是代表年份的四位數，範圍介於 1753 至 9999 之間。<br /><br /> MM 是代表指定年份中某個月份的兩位數，範圍介於 01 至 12 之間。<br /><br /> DD 是代表指定月份中某個日期的兩位數，範圍介於 01 至 31 之間 (視月份而定)。<br /><br /> hh 是代表小時的兩位數，範圍介於 00 至 23 之間。<br /><br /> mm 是代表分鐘的兩位數，範圍介於 00 至 59 之間。<br /><br /> ss 是代表秒鐘的兩位數，範圍介於 00 至 59 之間。<br /><br /> n* 是代表小數秒數的零至三位數，範圍介於 0 至 999 之間。|  
|字元長度|最小 19 個位置，最大 23 個位置|  
|儲存體大小|8 個位元組|  
|精確度|四捨五入成 .000、.003 或 .007 秒的遞增。|  
|預設值|1900-01-01 00:00:00|  
|日曆|西曆 (不含年份的完整範圍)。|  
|使用者自訂的小數秒數有效位數|否|  
|時區位移感知和保留|否|  
|日光節約感知|否|  
  
## <a name="supported-string-literal-formats-for-datetime"></a>支援 datetime 的字串常值格式  
下表列出支援的字串常值格式**datetime**。 除了 ODBC 以外， **datetime**字串常值是以單引號 （'），例如 'string_literaL'。 如果環境不是**us_english**，字串常值應該在格式 N 'string_literaL'。
  
|數值|Description|  
|---|---|
|日期格式：<br /><br /> [0]4/15/[19]96 -- (mdy)<br /><br /> [0]4-15-[19]96 -- (mdy)<br /><br /> [0]4.15.[19]96 -- (mdy)<br /><br /> [0]4/[19]96/15 -- (myd)<br /><br /> 15/[0]4/[19]96 -- (dmy)<br /><br /> 15/[19]96/[0]4 -- (dym)<br /><br /> [19]96/15/[0]4 -- (ydm)<br /><br /> [19]96/[0]4/15 -- (ymd)<br /><br /> 時間格式：<br /><br /> 14:30<br /><br /> 14:30[:20:999]<br /><br /> 14:30[:20.9]<br /><br /> 4am<br /><br /> 4 PM|您可以使用指定的數值月份來指定日期資料。 例如，5/20/97 代表 1997 年 5 月 20 日。 當您使用數值日期格式時，請在使用斜線 (/)、連字號 (-) 或句號 (.) 做為分隔符號的字串中指定月、日和年。 此字串必須以下列形式出現：<br /><br /> *數字分隔符號數字分隔符號數字 [時間] [時間]*<br /><br /> <br /><br /> 當語言設定為**us_english**，日期的預設順序是 mdy。 您可以使用來變更日期順序[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)陳述式。<br /><br /> SET DATEFORMAT 陳述式的設定會影響日期值的解譯方式。 如果順序與設定不符，就不會將值解譯為日期 (因為超出範圍)，否則這些值會被誤解。 例如，依 DATEFORMAT 設定而定，可以將 12/10/08 解譯為六種日期之一。 四部分的年份會解譯為年份。|  
  
|字母順序|Description|  
|---|---|
|Apr[il] [15][,] 1996<br /><br /> Apr[il] 15[,] [19]96<br /><br /> Apr[il] 1996 [15]<br /><br /> [15] Apr[il][,] 1996<br /><br /> 15 Apr[il][,][19]96<br /><br /> 15 [19]96 apr[il]<br /><br /> [15] 1996 apr[il]<br /><br /> 1996 APR[IL] [15]<br /><br /> 1996 [15] APR[IL]|您可以使用指定為完整月份名稱的月份來指定日期資料。 例如，April 或該月份在目前語言中指定的縮寫 Apr。逗號是選擇性且會忽略大小寫。<br /><br /> 以下是使用字母日期格式的一些指導方針：<br /><br /> 1） 將日期和時間資料括在單引號 （'）。 若為英文以外的語言，請使用 N'。<br /><br /> 2） 的字元括在括號是選擇性的。<br /><br /> 3） 如果您指定兩位數的年份，數值最後兩個值的數字小於[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)位於就與截止年份同一世紀的組態選項. 數值如果大於或等於這個選項的值，就在截止年份的前一個世紀。 例如，如果**兩位數年份的截止**是 2050 （預設值），25 會解譯為 2025年，而 50 則解譯為 1950年。 若要避免模糊不清，請使用四位數年份。<br /><br /> 4） 如果日的部分，就會提供每月的第一天。<br /><br /> <br /><br /> 如果以字母形式指定月份，就不適用 SET DATEFORMAT 工作階段設定。|  
  
|ISO 8601|Description|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.mmm]<br /><br /> YYYYMMDD[ hh:mm:ss[.mmm]]|範例:<br /><br /> 1) 2004年-05-23T14:25:10<br /><br /> 2) 2004年-05-23T14:25:10.487<br /><br /> <br /><br /> 若要使用 ISO 8601 格式，您必須在格式中指定每個元素。 這也包括**T**、 冒號 （:） 以及句號 （.） 格式所示。<br /><br /> 括號指出秒數部分的小數是選擇性的。 24 小時制格式指定時間元件。<br /><br /> T 表示的時間部分的開頭**datetime**值。<br /><br /> 使用 ISO 8601 格式的優點在於它是國際標準，而且沒有模糊不清的規格。 此外，此格式不受 SET DATEFORMAT 或[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)設定。|  
  
|未分隔|Description|  
|---|---|
|YYYYMMDD hh:mm:ss[.mmm]||  
  
|ODBC|Description|  
|---|---|
|{ ts '1998-05-02 01:23:56.123' }<br /><br /> { d '1990-10-02' }<br /><br /> { t '13:33:41' }|ODBC API 定義了逸出序列來代表日期和時間值，供 ODBC 呼叫時間戳記資料。 支援的 OLE DB 語言定義 (DBGUID-SQL) 也支援 ODBC 時間戳記格式[!INCLUDE[msCoName](../../includes/msconame-md.md)]OLE DB 提供者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 使用 ADO、OLE DB 與 ODBC 架構 API 的應用程式都可以使用這個 ODBC 時間戳記格式來代表日期和時間值。<br /><br /> ODBC 時間戳記逸出序列是的格式: { *literal_type* '*constant_value*'}:<br /><br /> <br /><br /> - *literal_type*指定逸出序列的類型。 時間戳記有三個*literal_type*規範：<br />1) d = 只有日期<br />2) t = 只有時間<br />3) ts = 時間戳記 （時間 + 日期）<br /><br /> <br /><br /> -'*constant_value*' 是逸出序列的值。 *constant_value*必須對每一個遵循這些格式*literal_type*。<br />d: yyyy-mm-dd<br />t: hh: mm: [.fff]<br />ts: yyyy-mm-dd hh: mm: [.fff]|  
  
## <a name="rounding-of-datetime-fractional-second-precision"></a>datetime 小數秒數有效位數的四捨五入  
**datetime**值會進位到.000、.003 或.007 秒的遞增下, 表所示。
  
|使用者指定的值|系統預存值|  
|---|---|
|01/01/98 23:59:59.999|1998-01-02 00:00:00.000|  
|01/01/98 23:59:59.995<br /><br /> 01/01/98 23:59:59.996<br /><br /> 01/01/98 23:59:59.997<br /><br /> 01/01/98 23:59:59.998|1998-01-01 23:59:59.997|  
|01/01/98 23:59:59.992<br /><br /> 01/01/98 23:59:59.993<br /><br /> 01/01/98 23:59:59.994|1998-01-01 23:59:59.993|  
|01/01/98 23:59:59.990<br /><br /> 01/01/98 23:59:59.991|1998-01-01 23:59:59.990|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 標準  
**datetime**不符合 ANSI 或 ISO 8601 相容。
  
##  <a name="_datetime"></a>將日期和時間資料轉換  
當您轉換成日期與時間資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕所有無法辨識為日期或時間的值。 使用 CAST 和 CONVERT 函數與日期和時間資料的相關資訊，請參閱[CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-other-date-and-time-types-to-the-datetime-data-type"></a>將其他日期與時間類型轉換成日期時間資料類型 
本章節描述當其他日期和時間資料類型會轉換成**datetime**資料型別。  
  
當轉換是來自**日期**，年、 月和日都會複製。 時間元件會設定為 00:00:00.000。 下列程式碼顯示將 `date` 值轉換成 `datetime` 值的結果。  
  
```sql
DECLARE @date date = '12-21-16';  
DECLARE @datetime datetime = @date;  
  
SELECT @datetime AS '@datetime', @date AS '@date';  
  
--Result  
--@datetime               @date  
------------------------- ----------  
--2016-12-21 00:00:00.000 2016-12-21  
```  
  
當轉換是來自**time （n)**、 時間元件會複製，而日期元件會設定為 ' 1900年-01-01'。 當小數有效位數**time （n)**值為大於三位數，此值會被截斷以符合。 下列範例顯示將 `time(4)` 值轉換成 `datetime` 值的結果。  
  
```sql
DECLARE @time time(4) = '12:10:05.1237';  
DECLARE @datetime datetime = @time;  
  
SELECT @datetime AS '@datetime', @time AS '@time';  
  
--Result  
--@datetime               @time  
------------------------- -------------  
--1900-01-01 12:10:05.123 12:10:05.1237  
```  
  
當轉換是來自**smalldatetime**，複製小時和分鐘。 秒和小數秒數會設定為 0。 下列程式碼顯示將 `smalldatetime` 值轉換成 `datetime` 值的結果。  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @datetime AS '@datetime', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetime               @smalldatetime  
------------------------- -----------------------  
--2016-12-01 12:32:00.000 2016-12-01 12:32:00  
```  
  
當轉換是來自**datetimeoffset （n)**，日期和時間元件都會複製。 時區則會被截斷。 當小數有效位數**datetimeoffset （n)**值大於三位數，此值會被截斷。 下列範例顯示將 `datetimeoffset(4)` 值轉換成 `datetime` 值的結果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1968-10-23 12:45:37.1234 +10:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetime AS '@datetime', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@datetime               @datetimeoffset  
------------------------- ------------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237 +01:0   
```  
  
當轉換是來自**datetime2**，會複製日期和時間。 當小數有效位數**datetime2**值大於三位數，此值會被截斷。 下列範例顯示將 `datetime2(4)` 值轉換成 `datetime` 值的結果。  
  
```sql
DECLARE @datetime2 datetime2(4) = '1968-10-23 12:45:37.1237';  
DECLARE @datetime datetime = @datetime2;  
  
SELECT @datetime AS '@datetime', @datetime2 AS '@datetime2';  
  
--Result  
--@datetime               @datetime2  
------------------------- ------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237  
```  
  
## <a name="examples"></a>範例  
下列範例會比較將字串轉換成每個結果**日期**和**時間**資料型別。
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|資料類型|輸出|  
|---|---|
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

