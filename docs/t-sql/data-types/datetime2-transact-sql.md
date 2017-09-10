---
title: "datetime2 (TRANSACT-SQL) |Microsoft 文件"
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
- datetime2
- datetime2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- dates [SQL Server], data types
- date and time [SQL Server], datetime2
- data types [SQL Server], date and time
- datetime2 data type [SQL Server]
ms.assetid: 868017f3-214f-43ef-8536-cc1632a2288f
caps.latest.revision: 58
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13766b3d0cb86780c2eca55c7f36e8fd16e973c5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2-transact-sql"></a>datetime2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定義日期，並結合了 24 小時制的時間。 **datetime2**可視為現有擴充**datetime**具有較大的日期範圍、 較大的預設小數有效位數和選擇性的使用者指定有效位數類型。
  
## <a name="datetime2-description"></a>datetime2 描述
  
|屬性|值|  
|--------------|-----------|  
|語法|**datetime2** [(*小數秒數有效位數*)]|  
|使用方式|宣告@MyDatetime2 **datetime2 （7)**<br /><br /> 建立資料表 Table1 (Column1 **datetime2 （7)** )|  
|預設的字串常值格式<br /><br /> (用於下層用戶端)|YYYY-MM-DD hh:mm:ss[.小數秒數]<br /><br /> 如需詳細資訊，請參閱下列的＜下層用戶端的回溯相容性＞一節。|  
|日期範圍|0001-01-01 到 31.12.99<br /><br /> 年 1 月 1，1 CE 到 9999 年 12 月 31 日 CE|  
|時間範圍|00:00:00 到 23:59:59.9999999|  
|時區位移範圍|無|  
|元素範圍|YYYY 是代表年份的四位數字，範圍介於 0001 至 9999 之間。<br /><br /> MM 是代表指定年份中某個月份的兩位數字，範圍介於 01 至 12 之間。<br /><br /> DD 是代表指定月份中某個日期的兩位數字，範圍介於 01 至 31 之間 (視月份而定)。<br /><br /> hh 是代表小時的兩位數字，範圍介於 00 至 23 之間。<br /><br /> mm 是代表分鐘的兩位數字，範圍介於 00 至 59 之間。<br /><br /> ss 是代表秒鐘的兩位數字，範圍介於 00 至 59 之間。<br /><br /> n* 是代表小數秒數的零至七位數字，範圍介於 0 至 9999999 之間。 Informatica，在小數秒數將會被截斷時 n > 3。|  
|字元長度|最小 19 個位置 (YYYY-MM-DD hh:mm:ss)，最大 27 個位置 (YYYY-MM-DD hh:mm:ss.0000000)|  
|有效位數，小數位數|0 至 7 位數，精確度為 100ns。 預設有效位數是 7 位數。|  
|儲存體大小|6 個位元組代表有效位數小於 3，而 7 個位元組則代表有效位數是 3 和 4。 所有其他有效位數則需要 8 個位元組。|  
|精確度|100 奈秒|  
|預設值|1900-01-01 00:00:00|  
|日曆|西曆|  
|使用者自訂的小數秒數有效位數|是|  
|時區位移感知和保留|否|  
|日光節約感知|否|  
  
資料型別中繼資料，請參閱[sys.systypes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)或[TYPEPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md). 有效位數和小數位數是某些日期和時間資料類型的變數。 若要取得的有效位數和小數位數的資料行，請參閱[COLUMNPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)， [COL_LENGTH &#40;TRANSACT-SQL &#41;](../../t-sql/functions/col-length-transact-sql.md)，或[sys.columns &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).
  
## <a name="supported-string-literal-formats-for-datetime2"></a>支援 datetime2 的字串常值格式
下表列出支援的 ISO 8601 和 ODBC 字串常值的格式**datetime2**。 如需字母、 數字、 未分隔和時間格式的日期和時間部分資訊**datetime2**，請參閱[日期 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/date-transact-sql.md)和[時間 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|[描述]|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> YYYY-MM-DDThh:mm:ss[.nnnnnnn]|此格式不受 SET LANGUAGE 和 SET DATEFORMAT 工作階段地區設定的影響。 **T**、 冒號 （:） 以及句號 （.） 會包含在字串常值，例如 ' 2007年-05-02T19:58:47.1234567'。|  
  
|ODBC|Description|  
|---|---|
|{ ts 'yyyy-mm-dd hh:mm:ss[.小數秒數]' }|ODBC API 專用：<br /><br /> 小數點右邊的位數 (代表小數秒數) 可指定為 0 至 7 (100 奈秒)。|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 相容性  
ANSI 和 ISO 8601 相容性的[日期](../../t-sql/data-types/date-transact-sql.md)和[時間](../../t-sql/data-types/time-transact-sql.md)套用至**datetime2**。
  
##  <a name="backward-compatibility-for-down-level-clients"></a>下層用戶端的回溯相容性  
有些下層用戶端不支援**時間**，**日期**， **datetime2**和**datetimeoffset**資料型別。 下表顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的上層執行個體與下層用戶端之間的類型對應。
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|傳遞至下層用戶端的預設字串常值格式|下層 ODBC|下層 OLEDB|下層 JDBC|下層 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetimeoffset**|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
  
## <a name="converting-date-and-time-data"></a>將日期和時間資料轉換
當您轉換成日期與時間資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕所有無法辨識為日期或時間的值。 使用 CAST 和 CONVERT 函數與日期和時間資料的相關資訊，請參閱[CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>將其他的日期和時間類型轉換為 datetime2 資料類型
本章節描述當其他日期和時間資料類型會轉換成**datetime2**資料型別。  
  
當轉換是來自**日期**，年、 月和日都會複製。  時間元件會設定為 00:00:00.0000000。  下列程式碼顯示將 `date` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
當轉換是來自**time （n)**、 時間元件會複製，而日期元件會設定為 ' 1900年-01-01'。 下列範例顯示將 `time(7)` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
當轉換是來自**smalldatetime**，複製小時和分鐘。 秒和小數秒數會設定為 0。 下列程式碼顯示將 `smalldatetime` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
當轉換是來自**datetimeoffset （n)**，日期和時間元件都會複製。 時區則會被截斷。 下列範例顯示將 `datetimeoffset(7)` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

當轉換是來自**datetime**，會複製日期和時間。  小數有效位數時間長達 7 位數。  下列範例顯示將 `datetime` 值轉換成 `datetime2` 值的結果。

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  
  
### <a name="converting-string-literals-to-datetime2"></a>將字串常值轉換為 datetime2  
如果整個字串皆是有效的格式，即可從字串常值轉換為日期與時間類型。 否則，就會引發執行階段錯誤。 從日期與時間類型轉換為字串常值的明確轉換不會指定樣式的隱含轉換，一律會採用目前工作階段的預設格式。 下表顯示的規則將字串轉換成常值**datetime2**資料型別。
  
|輸入字串常值|**datetime2**|  
|---|---|
|ODBC DATE|ODBC 字串常值會對應至**datetime**資料型別。 從 ODBC DATETIME 常值到任何指派作業**datetime2**型別會造成之間的隱含轉換**datetime**與此類型所定義的轉換規則。|  
|ODBC TIME|請參閱先前的 ODBC DATE 規則。|  
|ODBC DATETIME|請參閱先前的 ODBC DATE 規則。|  
|僅限 DATE|TIME 部分預設為 00:00:00。|  
|僅限 TIME|DATE 部分預設為 1900-1-1。|  
|僅限 TIMEZONE|提供預設值。|  
|DATE + TIME|一般|  
|DATE + TIMEZONE|不允許。|  
|TIME + TIMEZONE|DATE 部分預設為 1900-1-1。 忽略 TIMEZONE 輸入。|  
|DATE + TIME + TIMEZONE|將使用本機 DATETIME。|  
  
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
  
  

