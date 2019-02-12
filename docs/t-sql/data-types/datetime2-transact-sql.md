---
title: datetime2 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26d7b15318ccf171b8812449948ef0a04d17cfbd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039039"
---
# <a name="datetime2-transact-sql"></a>datetime2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定義日期，並結合了 24 小時制的時間。 **datetime2** 可視為現有 **datetime** 類型的延伸，因其具有較大的日期範圍、較大的預設小數有效位數和選擇性的使用者指定有效位數。
  
## <a name="datetime2-description"></a>datetime2 描述
  
|屬性|ReplTest1|  
|--------------|-----------|  
|語法|**datetime2** [ (*毫秒精確度*) ]|  
|使用方式|DECLARE \@MyDatetime2 **datetime2(7)**<br /><br /> CREATE TABLE Table1 ( Column1 **datetime2(7)** )|  
|預設的字串常值格式<br /><br /> (用於下層用戶端)|YYYY-MM-DD hh:mm:ss[.小數秒數]<br /><br /> 如需詳細資訊，請參閱下列的＜下層用戶端的回溯相容性＞一節。|  
|日期範圍|0001-01-01 到 31.12.99<br /><br /> 公元 1 年 1 月 1 日到公元 9999 年 12 月 31 日|  
|時間範圍|00:00:00 到 23:59:59.9999999|  
|時區位移範圍|None|  
|元素範圍|YYYY 是代表年份的四位數字，範圍介於 0001 至 9999 之間。<br /><br /> MM 是代表指定年份中某個月份的兩位數字，範圍介於 01 至 12 之間。<br /><br /> DD 是代表指定月份中某個日期的兩位數字，範圍介於 01 至 31 之間 (視月份而定)。<br /><br /> hh 是代表小時的兩位數字，範圍介於 00 至 23 之間。<br /><br /> mm 是代表分鐘的兩位數字，範圍介於 00 至 59 之間。<br /><br /> ss 是代表秒鐘的兩位數字，範圍介於 00 至 59 之間。<br /><br /> n* 是代表小數秒數的零至七位數字，範圍介於 0 至 9999999 之間。 在 Informatica 中，毫秒會在 n > 3 時遭到截斷。|  
|字元長度|最小 19 個位置 (YYYY-MM-DD hh:mm:ss)，最大 27 個位置 (YYYY-MM-DD hh:mm:ss.0000000)|  
|有效位數，小數位數|0 至 7 位數，精確度為 100ns。 預設有效位數是 7 位數。|  
|儲存體大小|6 個位元組代表有效位數小於 3，而 7 個位元組則代表有效位數是 3 和 4。 所有其他有效位數則需要 8 個位元組。|  
|精確度|100 奈秒|  
|預設值|1900-01-01 00:00:00|  
|日曆|西曆|  
|使用者自訂的小數秒數有效位數|是|  
|時區位移感知和保留|否|  
|日光節約感知|否|  
  
如需資料類型中繼資料，請參閱 [sys.systypes &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md) 或 [TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)。 有效位數和小數位數是某些日期和時間資料類型的變數。 若要取得資料行的有效位數和小數位數，請參閱 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)、[COL_LENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/col-length-transact-sql.md)，或 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)。
  
## <a name="supported-string-literal-formats-for-datetime2"></a>datetime2 支援的字串常值格式
下表列出 **datetime2** 支援的 ISO 8601 及 ODBC 字串常值格式。 如需 **datetime2** 日期和時間部分之字母、數字、未分隔及時間格式的資訊，請參閱 [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md) 和 [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)。
  
|ISO 8601|說明|  
|---|---|
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> YYYY-MM-DDThh:mm:ss[.nnnnnnn]|此格式不受 SET LANGUAGE 和 SET DATEFORMAT 工作階段地區設定的影響。 **T**、冒號 (:) 和句號 (.) 會包含在字串常值中，例如 '2007-05-02T19:58:47.1234567'。|  
  
|ODBC|Description|  
|---|---|
|{ ts 'yyyy-mm-dd hh:mm:ss[.小數秒數]' }|ODBC API 專用：<br /><br /> 小數點右邊的位數 (代表小數秒數) 可指定為 0 至 7 (100 奈秒)。|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 合規性  
[date](../../t-sql/data-types/date-transact-sql.md) 和 [time](../../t-sql/data-types/time-transact-sql.md) 的 ANSI 與 ISO 8601 合規性適用於 **datetime2**。
  
##  <a name="backward-compatibility-for-down-level-clients"></a>下層用戶端的回溯相容性  
有些下層用戶端不支援 **time**、**date**、**datetime2** 及 **datetimeoffset** 資料類型。 下表顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的上層執行個體與下層用戶端之間的類型對應。
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|傳遞至下層用戶端的預設字串常值格式|下層 ODBC|下層 OLEDB|下層 JDBC|下層 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
  
## <a name="converting-date-and-time-data"></a>轉換日期和時間資料
當您轉換成日期與時間資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕所有無法辨識為日期或時間的值。 如需 CAST 及 CONVERT 函式與日期和時間資料搭配使用的資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>將其他日期與時間類型轉換成 datetime2 資料類型
本節描述當其他日期與時間資料類型轉換成 **datetime2** 資料類型時，可能發生的狀況。  
  
當轉換來自 **date**，年、月和日都會複製。  時間元件會設定為 00:00:00.0000000。  下列程式碼顯示將 `date` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
從 **time(n)** 轉換時，會複製時間元件，而日期元件會設定為 '1900-01-01'。 下列範例顯示將 `time(7)` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
從 **smalldatetime** 轉換時，會複製小時和分鐘。 秒和小數秒數會設定為 0。 下列程式碼顯示將 `smalldatetime` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
從 **datetimeoffset(n)** 轉換時，會複製日期和時間元件。 時區則會被截斷。 下列範例顯示將 `datetimeoffset(7)` 值轉換成 `datetime2` 值的結果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

當轉換來自 **datetime**，會複製日期和時間。 小數有效位數會延伸至 7 位數。 下列範例顯示將 `datetime` 值轉換成 `datetime2` 值的結果。

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  

> [!NOTE]
> 在資料庫相容性層級 130 下，藉由考量小數部分的毫秒從 datetime 隱含轉換至 datetime2 資料類型顯示改善的精確度，會導致不同的轉換值，如上面範例所示。 只要 datetime 和 datetime2 資料類型之間存在混合的比較案例，就明確轉換為 datetime2 資料類型。 如需詳細資訊，請參閱此篇 [Microsoft 支援服務文章](https://support.microsoft.com/help/4010261)。

### <a name="converting-string-literals-to-datetime2"></a>將字串常值轉換為 datetime2  
如果整個字串皆是有效的格式，即可從字串常值轉換為日期與時間類型。 否則，就會引發執行階段錯誤。 從日期與時間類型轉換為字串常值的明確轉換不會指定樣式的隱含轉換，一律會採用目前工作階段的預設格式。 下表是字串常值轉換為 **datetime2** 資料類型的規則。
  
|輸入字串常值|**datetime2(n)**|  
|---|---|
|ODBC DATE|ODBC 字串常值會對應到 **datetime** 資料類型。 任何將 ODBC DATETIME 常值指派成 **datetime2** 類型的作業，皆會根據轉換規則，執行 **datetime** 與此類型之間的隱含轉換。|  
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
下列範例會比較將字串轉換成各種 **date** 和 **time** 資料類型的結果。
  
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
  
  
