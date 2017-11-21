---
title: "datetimeoffset (TRANSACT-SQL) |Microsoft 文件"
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
- datetimeoffset_TSQL
- datetimeoffset
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetimeoffset
- datetimeoffset data type [SQL Server]
- dates [SQL Server], data types
- data types [SQL Server], date and time
- time zones [SQL Server]
ms.assetid: a0455b71-ca25-476e-a7a8-0770f1860bb7
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a6c143380711d1af39a6c11f311e9ce3caf87c7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datetimeoffset-transact-sql"></a>datetimeoffset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

定義日期，並結合了具有時區感知並以 24 小時制為基礎的當日時間。
  
## <a name="datetimeoffset-description"></a>datetimeoffset 描述
  
|屬性|值|  
|---|---|
|語法|**datetimeoffset** [(*小數秒數有效位數*)]|  
|使用方式|宣告@MyDatetimeoffset **datetimeoffset(7)**<br /><br /> 建立資料表 Table1 (Column1 **datetimeoffset(7)** )|  
|預設的字串常值格式 (用於下層用戶端)|YYYY MM DD hh: mm: [.nnnnnnn] [{+ &#124;-} hh: mm]<br /><br /> 如需詳細資訊，請參閱下列的＜下層用戶端的回溯相容性＞一節。|  
|日期範圍|0001-01-01 到 31.12.99<br /><br /> 1 年 1 月 1 日到 9999 CE 的 CE 年 12 月 31 日|  
|時間範圍|00:00:00 到 23:59:59.9999999 （小數秒不支援在 Informatica）|  
|時區位移範圍|-14:00 到 + 14:00 （時區位移中會忽略 Informatica）|  
|元素範圍|YYYY 是代表年份的四位數，範圍介於 0001 至 9999 之間。<br /><br /> MM 是代表指定年份中某個月份的兩位數，範圍介於 01 至 12 之間。<br /><br /> DD 是代表指定月份中某個日期的兩位數，範圍介於 01 至 31 之間 (視月份而定)。<br /><br /> hh 是代表小時的兩位數，範圍介於 00 至 23 之間。<br /><br /> mm 是代表分鐘的兩位數，範圍介於 00 至 59 之間。<br /><br /> ss 是代表秒鐘的兩位數，範圍介於 00 至 59 之間。<br /><br /> n* 是代表小數秒數的零至七位數，範圍介於 0 至 9999999 之間。 Informatica 中不支援的小數秒數。<br /><br /> hh 是兩位數，範圍介於 -14 至 +14 之間。 Informatica 中，會忽略時區位移。<br /><br /> mm 是兩位數，範圍介於 00 至 59 之間。 Informatica 中，會忽略時區位移。|  
|字元長度|最小 26 位數 (YYYY MM DD hh: mm: {+ &#124;-} hh: mm)，最大 34 (YYYY-ss.nnnnnnn {+ &#124;-} hh: mm)|  
|有效位數，小數位數|請參閱下表。|  
|儲存體大小|10 個位元組 (固定) 是預設值，而且具有 100ns 小數秒數有效位數的預設值。|  
|精確度|100 奈秒|  
|預設值|1900-01-01 00:00:00 00:00|  
|日曆|西曆|  
|使用者自訂的小數秒數有效位數|是|  
|時區位移感知和保留|是|  
|日光節約感知|否|  
  
|指定的小數位數|結果 (有效位數，小數位數)|資料行長度 (以位元組為單位)|小數秒數有效位數|  
|---|---|---|---|
|**datetimeoffset**|(34,7)|10|7|  
|**datetimeoffset(0)**|(26,0)|8|0-2|  
|**datetimeoffset(1)**|(28,1)|8|0-2|  
|**datetimeoffset(2)**|(29,2)|8|0-2|  
|**datetimeoffset(3)**|(30,3)|9|3-4|  
|**datetimeoffset(4)**|(31,4)|9|3-4|  
|**datetimeoffset(5)**|(32,5)|10|5-7|  
|**datetimeoffset(6)**|(33,6)|10|5-7|  
|**datetimeoffset(7)**|(34,7)|10|5-7|  
  
## <a name="supported-string-literal-formats-for-datetimeoffset"></a>支援 datetimeoffset 的字串常值格式
下表列出支援的 ISO 8601 字串常值的格式**datetimeoffset**。 如需字母、 數字、 未分隔和時間格式的日期和時間部分資訊**datetimeoffset**，請參閱[日期 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/date-transact-sql.md)和[時間 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Description|  
|---|---|
|YYYY-MM-Yyyy-mm-ddthh [.nnnnnnn] [{+ &#124;-} hh: mm]|這兩種格式不受 SET LANGUAGE 和 SET DATEFORMAT 工作階段地區設定的影響。 之間不允許有空格**datetimeoffset**和**datetime**組件。|  
|YYYY-MM-DDThh:mm:ss[.nnnnnnn]Z (UTC)|根據 ISO 定義此格式表示**datetime**部分應該表示以國際標準時間 (UTC)。 例如，1999-12-12 12:30:30.12345 -07:00 應該表示成 1999-12-12 19:30:30.12345Z。|  
  
## <a name="time-zone-offset"></a>時區位移
時區位移指定為 UTC 的時區時差**時間**或**datetime**值。 時區位移可表示成 [+|-] hh:mm：
-   hh 是代表時區位移中時數的兩位數，範圍介於 00 至 14 之間。  
-   mm 是代表時區位移中額外分鐘數的兩位數，範圍介於 00 至 59 之間。  
-   \+（加號） 或 – （減號） 是時區時差的必要符號。 這會指出若要取得當地時間，則必須在 UTC 時間中加上或扣除時區位移。 時區位移的有效範圍介於 -14:00 至 +14:00 之間。  
  
時區位移範圍會遵循 XSD 結構描述定義的 W3C XML 標準，而且稍微與 SQL 2003 標準定義 (12:59 至 +14:00) 不同。
  
選擇性的型別參數*小數秒數有效位數*指定秒鐘小數部分的位數。 這個值可以是介於 0 至 7 (100 奈秒) 之間的整數。 預設值*小數秒數有效位數*為 100ns （秒鐘小數部分的七位數）。
  
這項資料會儲存於資料庫中，而且在伺服器中進行處理、比較、儲存和索引 (如同 UTC)。 時區位移將保留在資料庫中以便日後擷取。
  
指定的時區位移將假設為日光節約時間 (DST) 感知且經過調整任何給定的**datetime** DST 期間內。
  
如**datetimeoffset**類型，則 UTC 和當地 （永續或轉換的時區位移） **datetime** insert、 update、 算術、 convert 或指派作業期間，將會驗證值。 偵測到無效的 UTC 或當地 （永續或轉換的時區位移） **datetime**值將會引發無效值的錯誤。 例如，9999-12-31 10:10:00 在 UTC 中有效，但是在時區位移 +13:50 的當地時間中則會發生溢位。
  
若要將日期轉換成對應**datetimeoffset**值中的目標時區，請參閱[AT TIME ZONE &#40;TRANSACT-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md).
  
## <a name="ansi-and-iso-8601-compliance"></a>ANSI 和 ISO 8601 相容性  
ANSI 和 ISO 8601 標準區段[日期](../../t-sql/data-types/date-transact-sql.md)和[時間](../../t-sql/data-types/time-transact-sql.md)主題適用於**datetimeoffset**。
  
## <a name="backward-compatibility-for-down-level-clients"></a>下層用戶端的回溯相容性
有些下層用戶端不支援**時間**，**日期**， **datetime2**和**datetimeoffset**資料型別。 下表顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的上層執行個體與下層用戶端之間的類型對應。
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|傳遞至下層用戶端的預設字串常值格式|下層 ODBC|下層 OLEDB|下層 JDBC|下層 SQLCLIENT|  
|---|---|---|---|---|---|
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetimeoffset**|YYYY MM DD hh: mm: [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
  
## <a name="converting-date-and-time-data"></a>將日期和時間資料轉換
當您轉換成日期與時間資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕所有無法辨識為日期或時間的值。 使用 CAST 和 CONVERT 函數與日期和時間資料的相關資訊，請參閱[CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
當轉換成**日期**，年、 月和日都會複製。 下列程式碼顯示將 `datetimeoffset(4)` 值轉換成 `date` 值的結果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10 +01:00';  
DECLARE @date date= @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @date AS 'date';  
  
--Result  
--@datetimeoffset                date  
-------------------------------- ----------  
--2025-12-10 12:32:10.0000 +01:0 2025-12-10  
--  
--(1 row(s) affected)  
  
```  
  
如果會轉換為**time （n)**，我們、 分鐘、 秒和小數秒數會複製。 時區值則會被截斷。 當的有效位數**datetimeoffset （n)**值的有效位數大於**time （n)**值，此值會無條件進位。 下列程式碼顯示將 `datetimeoffset(4)` 值轉換成 `time(3)` 值的結果。
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @time time(3) = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @time AS 'time';  
  
--Result  
--@datetimeoffset                time  
-------------------------------- ------------  
-- 2025-12-10 12:32:10.1237 +01:00    12:32:10.124  
  
--  
--(1 row(s) affected)  
  
```  
  
當轉換成**datetime**、 日期和時間值會複製，而且時區會被截斷。 當小數有效位數**datetimeoffset （n)**值大於三位數，則會截斷值。 下列程式碼顯示將 `datetimeoffset(4)` 值轉換成 `datetime` 值的結果。
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '12-10-25 12:32:10.1237 +01:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset ', @datetime AS 'datetime';  
  
--Result  
--@datetimeoffset                datetime  
-------------------------------- -----------------------  
--2025-12-10 12:32:10.1237 +01:0 2025-12-10 12:32:10.123  
--  
--(1 row(s) affected)  
```  
  
轉換**smalldatetime**，會複製日期和時間。 分鐘會根據秒值四捨五入，而秒會設定為 0。 下列程式碼顯示將 `datetimeoffset(3)` 值轉換成 `smalldatetime` 值的結果。  
  
```sql
DECLARE @datetimeoffset datetimeoffset(3) = '1912-10-25 12:24:32 +10:0';  
DECLARE @smalldatetime smalldatetime = @datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetimeoffset                @smalldatetime  
-------------------------------- -----------------------  
--1912-10-25 12:24:32.000 +10:00 1912-10-25 12:25:00  
--  
--(1 row(s) affected)  
```  
  
如果會轉換為**datetime2**，日期和時間會複製到**datetime2**截斷值，以及時區。 當的有效位數**datetime2**值的有效位數大於**datetimeoffset （n)**值，小數秒會截斷以符合。 下列程式碼顯示將 `datetimeoffset(4)` 值轉換成 `datetime2(3)` 值的結果。
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1912-10-25 12:24:32.1277 +10:0';  
DECLARE @datetime2 datetime2(3)=@datetimeoffset;  
  
SELECT @datetimeoffset AS '@datetimeoffset', @datetime2 AS '@datetime2';  
  
--Result  
@datetimeoffset                    @datetime2  
---------------------------------- ----------------------  
1912-10-25 12:24:32.1277 +10:00    1912-10-25 12:24:32.12  
  
--(1 row(s) affected)  
```  
  
### <a name="converting-datetimeoffset-data-type-to-other-date-and-time-types"></a>將 datetimeoffset 資料類型到其他的日期和時間類型轉換
下表說明發生的狀況時**datetimeoffset**資料類型已轉換成其他日期和時間資料類型。
  
### <a name="converting-string-literals-to-datetimeoffset"></a>將字串常值轉換成 datetimeoffset
如果整個字串皆是有效的格式，即可從字串常值轉換為日期與時間類型。 否則，就會引發執行階段錯誤。 從日期與時間類型轉換為字串常值的明確轉換不會指定樣式的隱含轉換，一律會採用目前工作階段的預設格式。 下表顯示的規則將字串轉換成常值**datetimeoffset**資料型別。
  
|輸入字串常值|**datetimeoffset （n)**|  
|---|---|
|ODBC DATE|ODBC 字串常值會對應至**datetime**資料型別。 從 ODBC DATETIME 常值到任何指派作業**datetimeoffset**型別會造成之間的隱含轉換**datetime**與此類型所定義的轉換規則。|  
|ODBC TIME|請參閱先前的 ODBC DATE 規則。|  
|ODBC DATETIME|請參閱先前的 ODBC DATE 規則。|  
|僅限 DATE|TIME 部分預設為 00:00:00。 TIMEZONE 預設為 +00:00。|  
|僅限 TIME|DATE 部分預設為 1900-1-1。 TIMEZONE 將預設為 +00:00。|  
|僅限 TIMEZONE|提供預設值|  
|DATE + TIME|TIMEZONE 預設為 +00:00。|  
|DATE + TIMEZONE|不允許|  
|TIME + TIMEZONE|DATE 部分預設為 1900-1-1。|  
|DATE + TIME + TIMEZONE|一般|  
  
## <a name="examples"></a>範例  
下列範例會比較將字串轉換成每個結果**日期**和**時間**資料型別。
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset'  
    ,CAST('2007-05-08 12:35:29.1234567+12:15' AS datetimeoffset(7)) AS  
        'datetimeoffset IS08601';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|資料類型|輸出|  
|---|---|
|**Time**|12:35:29. 1234567|  
|**日期**|2007-05-08|  
|**Smalldatetime**|2007-05-08 12:35:00|  
|**Datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**Datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>另請參閱
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[TIME ZONE &AMP; #40;TRANSACT-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  

