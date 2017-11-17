---
title: "日期 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- date_TSQL
- date
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], date
- date and time [SQL Server], date
- dates [SQL Server], data types
- date data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: c963e8b4-5a85-4bd0-9d48-3f8da8f6516b
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c5d3a52b6163f375850b22e27baf9a858ef8ed8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="date-transact-sql"></a>日期 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的日期。
  
## <a name="date-description"></a>date 描述
  
|屬性|值|  
|--------------|-----------|  
|語法|**date**|  
|使用方式|宣告@MyDate**日期**<br /><br /> 建立資料表 Table1 (Column1**日期**)|  
|預設的字串常值格式<br /><br /> (用於下層用戶端)|YYYY-MM-DD<br /><br /> 如需詳細資訊，請參閱下列的＜下層用戶端的回溯相容性＞一節。|  
|範圍|0001-01-01 到 9999-12-31 (1582年-10-15 到 9999-12-31 的 Informatica)<br /><br /> 1 年 1 月 1 日到 9999 CE （年 12 月 31，1582 年 10 月 15 號 CE，Informatica 的 9999 CE） 的 CE 年 12 月 31 日|  
|元素範圍|YYYY 是代表年份的四位數，範圍介於 0001 至 9999 之間。 Informatica，如 YYYY 限於 1582年到 9999 的範圍。<br /><br /> MM 是代表指定年份中某個月份的兩位數，範圍介於 01 至 12 之間。<br /><br /> DD 是代表指定月份中某個日期的兩位數，範圍介於 01 至 31 之間 (視月份而定)。|  
|字元長度|10 個位置|  
|有效位數，小數位數|10, 0|  
|儲存體大小|3 個位元組 (固定)|  
|儲存體結構|1 個 3 位元組的整數會儲存日期。|  
|精確度|一天|  
|預設值|1900-01-01<br /><br /> 這個值會用於從隱含轉換附加的日期部分**時間**至**datetime2**或**datetimeoffset**。|  
|日曆|西曆|  
|使用者自訂的小數秒數有效位數|否|  
|時區位移感知和保留|否|  
|日光節約感知|否|  
  
## <a name="supported-string-literal-formats-for-date"></a>支援字串常值格式的日期
下表顯示有效的字串常值格式**日期**資料型別。
  
|數值|Description|  
|-------------|-----------------|  
|mdy<br /><br /> [m] m/dd / [yy] yy<br /><br /> [m] m-dd-[yy] yy<br /><br /> [m]m.dd。[yy] yy<br /><br /> myd<br /><br /> mm / yy/dd [yy]<br /><br /> mm-[yy] yy/dd<br /><br /> [m] m [yy] yy.dd<br /><br /> dmy<br /><br /> dd / [m] m / [yy] yy<br /><br /> dd-[m] m-[yy] yy<br /><br /> dd [m] m [yy] yy<br /><br /> dym<br /><br /> dd / [yy] yy / [m] m<br /><br /> dd-[yy] yy-[m] m<br /><br /> dd [yy] yy。[m] m<br /><br /> ymd<br /><br /> [yy] yy / [m] m/dd<br /><br /> [yy] yy-[m] m-dd<br /><br /> [yy] yy-[m] m-dd|[m]m、dd 和 [yy]yy 在字串中代表月、日和年，並且使用斜線 (/)、連字號 (-) 或句號 (.) 做為分隔符號。<br /><br /> 僅支援四或兩位數年份。 請盡可能使用四位數年份。 若要指定介於 0001 到 9999 之間整數，表示為兩位數年份解譯為四位數年份的截止年份，請使用[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)。<br /><br /> **注意！** Informatica，如 YYYY 限於 1582年到 9999 的範圍。<br /><br /> 兩位數年份若小於或等於截止年份的後兩位數，表示它與截止年份同一世紀。 兩位數年份若大於截止年份的後兩位數，表示它在截止年份的前一個世紀。 例如，如果兩位數年份的截止是預設值 2049，則兩位數年份 49 就會被解譯為 2049，而兩位數年份 50 則解譯為 1950。<br /><br /> 預設的日期格式由目前的語言設定決定。 您可以使用來變更日期格式[SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)和[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)陳述式。<br /><br /> **Ydm**格式不支援**日期**。|  
  
|字母順序|Description|  
|------------------|-----------------|  
|mon [dd] [，] yyyy<br /><br /> mon dd [，] [yy] yy<br /><br /> mon yyyy [dd]<br /><br /> [dd] mon [，] yyyy<br /><br /> dd mon [，] [yy] yy<br /><br /> dd [yy] yy mon<br /><br /> [dd] yyyy mon<br /><br /> yyyy mon [dd]<br /><br /> yyyy [dd] mon|**mon**代表完整月份名稱或目前的語言中月份縮寫。 逗號是選擇性且會忽略大小寫。<br /><br /> 若要避免模糊不清，請使用四位數年份。<br /><br /> 如果漏了日的部分，就用當月第一天。|  
  
|ISO 8601|描述|  
|--------------|----------------|  
|YYYY-MM-DD<br /><br /> YYYYMMDD|與 SQL 標準相同。 這是定義為國際標準的唯一格式。|  
  
|未分隔|Description|  
|-----------------|-----------------|  
|[yy] yymmdd<br /><br /> yyyy [dd] [mm]|**日期**資料可以指定四、 六或八個位數。 六個或 8 位數字串一律解譯為**ymd**。 月和日一定是兩位數。 四位數字串則會解譯為年份。|  
  
|ODBC|Description|  
|----------|-----------------|  
|{d ' yyyy-mm-dd'}|ODBC API 專用。|  
  
|W3C XML 格式|Description|  
|--------------------|-----------------|  
|yyyy-mm-ddTZD|特別支援 XML / SOAP 使用方式。<br /><br /> TZD 是時區指示項 (Z 或 + hh: mm 或 -hh:mm)：<br /><br /> -hh: mm 代表時區位移。 hh 表示時區時差中的兩位數時數，範圍介於 0 至 14 之間。<br />-MM 是兩位數，範圍從 0 到 59，代表時區位移中額外分鐘數。<br />-+ （加號） 或 – （減號） 的時區時差的必要符號。 這會指出若要取得當地時間，則必須在國際標準時間 (UTC) 中加上或扣除時區位移。 時區位移的有效範圍介於 -14:00 至 +14:00 之間。|  
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 相容性  
**日期**符合西曆的 ANSI SQL 標準定義: 「 附註 85-Datetime 資料類型會將日期允許採用西曆格式儲存日期範圍 0001 – 01 – 01 ce 到 9999 – 12 – 31 CE。 」
  
下層用戶端所使用的預設字串常值格式，會遵循 SQL 標準格式定義 YYYY-MM-DD。 此格式與 ISO 8601 所定義的 DATE 相同。
  
> [!NOTE]  
>  Informatica 的範圍限於 1582年-10-15 (，1582 年 10 月 15 號 CE) 至 9999-12-31 (年 12 月 31 日到 9999 CE)。  
  
## <a name="backward-compatibility-for-down-level-clients"></a>下層用戶端的回溯相容性
有些下層用戶端不支援**時間**，**日期**， **datetime2**和**datetimeoffset**資料型別。 下表顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的上層執行個體與下層用戶端之間的類型對應。
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|傳遞至下層用戶端的預設字串常值格式|下層 ODBC|下層 OLEDB|下層 JDBC|下層 SQLCLIENT|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetimeoffset**|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
  
## <a name="converting-date-and-time-data"></a>將日期和時間資料轉換
當您轉換成日期與時間資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕所有無法辨識為日期或時間的值。 使用 CAST 和 CONVERT 函數與日期和時間資料的相關資訊，請參閱[CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
當轉換為**time （n)**，轉換失敗，並會引發錯誤訊息 206: 「 運算元類型衝突： date 與 time 不相容 」。
  
如果會轉換為**datetime**、 將會複製日期和時間元件設定為 00:00:00.000。 下列程式碼顯示將 `date` 值轉換成 `datetime` 值的結果。  
  
```sql
DECLARE @date date= '12-10-25';  
DECLARE @datetime datetime= @date;  
  
SELECT @date AS '@date', @datetime AS '@datetime';  
  
--Result  
--@date      @datetime  
------------ -----------------------  
--2025-12-10 2025-12-10 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
在轉換成**smalldatetime**，當**日期**範圍中的值是[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)，日期元件會複製，而時間元件會設定為00:00:00。 時**日期**值超出範圍**smalldatetime** ，就會引發錯誤訊息 242 的值:"的轉換**日期**資料型別**smalldatetime**資料類型的結果超出範圍的值; 而**smalldatetime**值設定為 NULL。 下列程式碼顯示將 `date` 值轉換成 `smalldatetime` 值的結果。
  
```sql
DECLARE @date date= '1912-10-25';  
DECLARE @smalldatetime smalldatetime = @date;  
  
SELECT @date AS '@date', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@date      @smalldatetime  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00  
--  
--(1 row(s) affected)  
```  
  
當轉換為**datetimeoffset （n)**會複製日期，且時間會設定為 00: 00.0000000 + 00:00。 下列程式碼顯示將 `date` 值轉換成 `datetimeoffset(3)` 值的結果。
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetimeoffset datetimeoffset(3) = @date;  
  
SELECT @date AS '@date', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@date      @datetimeoffset  
------------ ------------------------------  
--1912-10-25 1912-10-25 00:00:00.000 +00:00  
--  
--(1 row(s) affected)  
```  
  
如果會轉換為**datetime2**會複製日期元件，且時間元件設定為 00:00:00.00 (n) 的值為何。 下列程式碼顯示將 `date` 值轉換成 `datetime2(3)` 值的結果。
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.00  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-date-to-other-date-and-time-types"></a>將日期轉換成其他日期和時間類型
本章節描述發生的狀況時**日期**資料類型已轉換成其他日期和時間資料類型。
  
當轉換為**time （n)**，轉換失敗，並會引發錯誤訊息 206: 「 運算元類型衝突： date 與 time 不相容 」。
  
如果會轉換為**datetime**，將會複製日期。 下列程式碼顯示將 `date` 值轉換成 `datetime` 值的結果。
  
```sql
DECLARE @date date= '12-10-25';  
DECLARE @datetime datetime= @date;  
  
SELECT @date AS '@date', @datetime AS '@datetime';  
  
--Result  
--@date      @datetime  
------------ -----------------------  
--2025-12-10 2025-12-10 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
當轉換為**smalldatetime**、**日期**範圍中的值是[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)，日期元件會複製，而時間元件會設定為00:00:00.000。 當**日期**值超出範圍**smalldatetime**引發值、 錯誤訊息 242: 「 日期資料類型轉換成 smalldatetime 資料類型時，產生超出範圍的值。";和**smalldatetime**值設定為 NULL。 下列程式碼顯示將 `date` 值轉換成 `smalldatetime` 值的結果。
  
```sql
DECLARE @date date= '1912-10-25';  
DECLARE @smalldatetime smalldatetime = @date;  
  
SELECT @date AS '@date', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@date      @smalldatetime  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00  
--  
--(1 row(s) affected)  
```  
  
要轉換**datetimeoffset （n)**會複製日期，且時間會設定為 00: 00.0000000 + 00:00。 下列程式碼顯示將 `date` 值轉換成 `datetimeoffset(3)` 值的結果。
  
```sql
DECLARE @date date = '1912-10-25';  
DECLARE @datetimeoffset datetimeoffset(3) = @date;  
  
SELECT @date AS '@date', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@date      @datetimeoffset  
------------ ------------------------------  
--1912-10-25 1912-10-25 00:00:00.000 +00:00  
--  
--(1 row(s) affected)  
```  
  
當轉換為**datetime2**，會複製日期元件，而時間元件會設定為 00: 00.000000。 下列程式碼顯示將 `date` 值轉換成 `datetime2(3)` 值的結果。
  
```sql
DECLARE @date date = '1912-10-25'  
DECLARE @datetime2 datetime2(3) = @date;  
  
SELECT @date AS '@date', @datetime2 AS '@datetime2(3)';  
  
--Result  
--@date      @datetime2(3)  
------------ -----------------------  
--1912-10-25 1912-10-25 00:00:00.000  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-date"></a>將字串常值轉換成日期
如果整個字串皆是有效的格式，即可從字串常值轉換為日期與時間類型。 否則，就會引發執行階段錯誤。 從日期與時間類型轉換為字串常值的明確轉換不會指定樣式的隱含轉換，一律會採用目前工作階段的預設格式。 下表顯示的規則將字串轉換成常值**日期**資料型別。
  
|輸入字串常值|**date**|  
|---|---|
|ODBC DATE|ODBC 字串常值會對應至**datetime**資料型別。 從 ODBC DATETIME 常值到任何指派作業**日期**型別會造成之間的隱含轉換**datetime**與此類型所定義的轉換規則。|  
|ODBC TIME|請參閱先前的 ODBC DATE 規則。|  
|ODBC DATETIME|請參閱先前的 ODBC DATE 規則。|  
|僅限 DATE|一般|  
|僅限 TIME|提供預設值。|  
|僅限 TIMEZONE|提供預設值。|  
|DATE + TIME|使用輸入字串的 DATE 部分。|  
|DATE + TIMEZONE|不允許。|  
|TIME + TIMEZONE|提供預設值。|  
|DATE + TIME + TIMEZONE|使用本機 DATETIME 的 DATE 部分。|  
  
## <a name="examples"></a>範例  
下列範例會比較將字串轉換成各種 date 與 time 資料類型的結果。
  
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
|---------------|------------|  
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

