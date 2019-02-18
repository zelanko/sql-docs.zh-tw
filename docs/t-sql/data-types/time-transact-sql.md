---
title: time (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- time_TSQL
- time
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- time [SQL Server]
- date and time [SQL Server], time
- data types [SQL Server], date and time
- time data type [SQL Server]
ms.assetid: 30a6c681-8190-48e4-94d0-78182290a402
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03f63929d54039399a292e086315c0b8d660f206
ms.sourcegitcommit: bbdf51f0d56acfa6bcc4a5c4fe2c9f3cd4225edc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56079454"
---
# <a name="time-transact-sql"></a>時間 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  定義一天的時間。 這個時間不含時區感知，而且是以 24 小時制為基礎。  
  
  > [!NOTE]  
  > Informatica 資訊會提供給使用 Informatica Connector 的 PDW 客戶。 
  
## <a name="time-description"></a>time 描述  
  
|屬性|ReplTest1|  
|--------------|-----------|  
|語法|**time** [ (*毫秒小數位數*) ]|  
|使用方式|DECLARE \@MyTime **time(7)**<br /><br /> CREATE TABLE Table1 ( Column1 **time(7)** )|  
|*毫秒小數位數*|指定秒鐘小數部分的位數。<br /><br /> 這可以是介於 0 至 7 之間的整數。 針對 Informatica，這可以是介於 0 至 3 之間的整數。<br /><br /> 預設的小數位數是 7 (100 毫秒)。|  
|預設的字串常值格式<br /><br /> (用於下層用戶端)|Informatica 為 hh:mm:ss[.nnnnnnn])<br /><br /> 如需詳細資訊，請參閱[下層用戶端的回溯相容性](#BackwardCompatibilityforDownlevelClients)一節。|  
|範圍|00:00:00.0000000 到 23:59:59.9999999 (Informatica 為 00:00:00.000 到 23:59:59.999)|  
|元素範圍|hh 是代表小時的兩位數，範圍介於 0 至 23 之間。<br /><br /> mm 是代表分鐘的兩位數，範圍介於 0 至 59 之間。<br /><br /> ss 是代表秒鐘的兩位數，範圍介於 0 至 59 之間。<br /><br /> n\* 是代表毫秒的零至七位數，範圍介於 0 至 9999999 之間。 針對 Informatica，n\* 為 0 到 3 位數，範圍為 0 至 999。|  
|字元長度|最小 8 個位置 (hh:mm:ss)，最大 16 個位置 (hh:mm:ss.nnnnnnn)。 針對 Informatica，最大值為 12 (hh:mm:ss.nnn)。|  
|有效位數，小數位數<br /><br /> (使用者僅指定小數位數)|請參閱下表。|  
|儲存體大小|固定的 5 個位元組是具有預設 100ns 小數秒數有效位數的預設值。 在 Informatica 中，預設為 4 個位元組、固定，並具有預設 1ms 毫秒精確度。|  
|精確度|100 奈秒 (Informatica 中為 1 毫秒)|  
|預設值|00:00:00<br /><br /> 這個值會用於從 **date** 隱含轉換成 **datetime2** 或 **datetimeoffset** 的附加時間部分。|  
|使用者自訂的小數秒數有效位數|是|  
|時區位移感知和保留|否|  
|日光節約感知|否|  
  
|指定的小數位數|結果 (有效位數，小數位數)|資料行長度 (以位元組為單位)|小數<br /><br /> seconds<br /><br /> 有效位數|  
|---------------------|---------------------------------|-----------------------------|------------------------------------------|  
|**time**|(16,7) [Informatica 中為 (12,3)]|5 (Informatica 中為 4)|7 (Informatica 中為 3)|  
|**time(0)**|(8,0)|3|0-2|  
|**time(1)**|(10,1)|3|0-2|  
|**time(2)**|(11,2)|3|0-2|  
|**time(3)**|(12,3)|4|3-4|  
|**time(4)**<br /><br /> Informatica 中不支援此項目。|(13,4)|4|3-4|  
|**time(5)**<br /><br /> Informatica 中不支援此項目。|(14,5)|5|5-7|  
|**time(6)**<br /><br /> Informatica 中不支援此項目。|(15,6)|5|5-7|  
|**time(7)**<br /><br /> Informatica 中不支援此項目。|(16,7)|5|5-7|  
  
## <a name="supported-string-literal-formats-for-time"></a>支援 time 的字串常值格式  
 下表顯示 **time** 資料類型的有效字串常值格式。  
  
|[SQL Server]|Description|  
|----------------|-----------------|  
|hh:mm[:ss][:小數秒數][AM][PM]<br /><br /> hh:mm[:ss][.小數秒數][AM][PM]<br /><br /> hhAM[PM]<br /><br /> hh AM[PM]|無論您是否指定 AM，只要小時的值為 0 就表示午夜之後 (AM) 的小時。 小時等於 0 時，無法指定 PM。<br /><br /> 如果沒有指定 AM 或 PM，小時值 01 至 11 就代表正午之前的小時。 指定為 AM 時，這些值就代表正午之前的小時。 如果指定為 PM，這些值就代表正午之後的小時。<br /><br /> 如果沒有指定 AM 或 PM，小時值 12 就代表從正午開始的小時。 如果指定為 AM，此值就代表從午夜開始的小時。 如果指定為 PM，此值就代表從正午開始的小時。 例如，12:01 就是正午之後的 1 分鐘，也就是 12:01 PM，而 12:01 AM 則是午夜之後一分鐘。 指定為 12:01 AM 與指定為 00:01 或 00:01 AM 是相同的。<br /><br /> 如果未指定 AM 或 PM，從 13 到 23 的小時值就代表正午之後的小時。 如果指定為 PM，這些值也代表正午之後的小時。 當小時值為 13 至 23 時，則無法指定為 AM。<br /><br /> 24 小時值無效。 若要表示午夜，請使用 12: 00 AM 或 00:00。<br /><br /> 毫秒前可以用冒號 (:) 或句號 (.)。 如果使用冒號，數字是指千分之一秒。 如果使用句號，一位數代表十分之一秒、二位數代表百分之一秒，而三位數代表千分之一秒。 例如，12:30:20:1 表示 12:30 過 20 又千分之一秒；12:30:20.1 表示 12:30 過 20 又十分之一秒。|  
  
|ISO 8601|注意|  
|--------------|-----------|  
|hh:mm:ss<br /><br /> hh:mm[:ss][.小數秒數]|hh 表示時區時差中的兩位數時數，範圍介於 0 至 14 之間。<br /><br /> mm 是代表時區位移中額外分鐘數的兩位數，範圍介於 0 至 59 之間。|  
  
|ODBC|注意|  
|----------|-----------|  
|{t 'hh:mm:ss[.小數秒數]'}|ODBC API 專用。|  
  
## <a name="compliance-with-ansi-and-iso-8601-standards"></a>符合 ANSI 和 ISO 8601 標準  
 為了達成回溯相容並與現有日期和時間類型一致，因此不支援使用 24 小時制來代表午夜和超過 59 的閏秒 (如 ISO 8601 (5.3.2 和 5.3) 所定義)。  
  
 預設字串常值格式 (用於下層用戶端) 將會符合 SQL 標準格式 (定義為 hh:mm:ss[.nnnnnnn])。 這種格式與 TIME 的 ISO 8601 定義很相似 (不含小數秒數)。  
  
##  <a name="BackwardCompatibilityforDownlevelClients"></a> 下層用戶端的回溯相容性  
 有些下層用戶端不支援 **time**、**date**、**datetime2** 及 **datetimeoffset** 資料類型。 下表顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的上層執行個體與下層用戶端之間的類型對應。  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型|傳遞至下層用戶端的預設字串常值格式|下層 ODBC|下層 OLEDB|下層 JDBC|下層 SQLCLIENT|  
|-----------------------------------------|----------------------------------------------------------------|----------------------|-----------------------|----------------------|---------------------------|  
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetime2**|YYYY-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
|**datetimeoffset**|YYYY-MM-DD hh:mm:ss[.nnnnnnn] [+&#124;-]hh:mm|SQL_WVARCHAR 或 SQL_VARCHAR|DBTYPE_WSTR 或 DBTYPE_STR|Java.sql.String|字串或 SqString|  
  
## <a name="converting-date-and-time-data"></a>轉換日期和時間資料  
 當您轉換成日期與時間資料類型時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕所有無法辨識為日期或時間的值。 如需 CAST 及 CONVERT 函式與日期和時間資料搭配使用的資訊，請參閱 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
### <a name="converting-timen-data-type-to-other-date-and-time-types"></a>將 time(n) 資料類型轉換成其他日期與時間類型  
 本節描述當 **time** 資料類型轉換成其他日期和時間資料類型時，可能發生的狀況。  
  
 當轉換成 **time(n)** 時，時、分和秒都會複製。 當目標有效位數小於來源有效位數時，毫秒將會四捨五入，以配合目標有效位數。 下列範例顯示將 `time(4)` 值轉換成 `time(3)` 值的結果。  
  
```  
DECLARE @timeFrom time(4) = '12:34:54.1237';  
DECLARE @timeTo time(3) = @timeFrom;  
  
SELECT @timeTo AS 'time(3)', @timeFrom AS 'time(4)';  
  
--Results  
--time(3)      time(4)  
-------------- -------------  
--12:34:54.124 12:34:54.1237  
--  
--(1 row(s) affected)  
```  
  
 如果轉換目標為 **date**，轉換會失敗，並引發錯誤訊息 206：「運算元類型衝突：date 與 time 不相容」。  
  
 當轉換成 **datetime** 時，將會複製時、分和秒的值，而且日期元件會設定為 '1900-01-01'。 如果 **time(n)** 值的毫秒精確度大於三位數，**datetime** 結果將會被截斷。 下列程式碼顯示將 `time(4)` 值轉換成 `datetime` 值的結果。  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime datetime= @time;  
SELECT @time AS '@time', @datetime AS '@datetime';  
  
--Result  
--@time         @datetime  
--------------- -----------------------  
--12:15:04.1237 1900-01-01 12:15:04.123  
--  
--(1 row(s) affected)  
  
```  
  
 當轉換成 **smalldatetime** 時，日期會設定為 '1900-01-01'，而小時和分鐘值會四捨五入。 秒和小數秒數會設定為 0。 下列程式碼顯示將 `time(4)` 值轉換成 `smalldatetime` 值的結果。  
  
```  
-- Shows rounding up of the minute value.  
DECLARE @time time(4) = '12:15:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';   
  
--Result  
@time            @smalldatetime  
---------------- -----------------------  
12:15:59.9999    1900-01-01 12:16:00--  
--(1 row(s) affected)  
  
-- Shows rounding up of the hour value.  
DECLARE @time time(4) = '12:59:59.9999';   
DECLARE @smalldatetime smalldatetime= @time;    
  
SELECT @time AS '@time', @smalldatetime AS '@smalldatetime';  
@time            @smalldatetime  
---------------- -----------------------  
12:59:59.9999    1900-01-01 13:00:00  
  
(1 row(s) affected)  
  
```  
  
 當轉換成 **datetimeoffset(n)** 時，日期會設定為 '1900-01-01'，時間則會複製。 時區時差會設定為 +00:00。 如果 **time(n)** 值的毫秒精確度大於 **datetimeoffset(n)** 值的有效位數，此值會四捨五入以配合其大小。 下列範例顯示將 `time(4)` 值轉換成 `datetimeoffset(3)` 類型的結果。  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetimeoffset datetimeoffset(3) = @time;  
  
SELECT @time AS '@time', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@time         @datetimeoffset  
--------------- ------------------------------  
--12:15:04.1237 1900-01-01 12:15:04.124 +00:00  
--  
--(1 row(s) affected)  
  
```  
  
 當轉換成 **datetime2(n)** 時，日期會設定為 '1900-01-01' 且會複製時間元件，而時區位移會設定為 00:00。 如果 **datetime2(n)** 值的毫秒精確度大於 **time(n)** 值，此值將會四捨五入以配合其大小。  下列範例顯示將 `time(4)` 值轉換成 `datetime2(2)` 值的結果。  
  
```  
DECLARE @time time(4) = '12:15:04.1237';  
DECLARE @datetime2 datetime2(3) = @time;  
  
SELECT @datetime2 AS '@datetime2', @time AS '@time';  
  
--Result  
--@datetime2              @time  
------------------------- -------------  
--1900-01-01 12:15:04.124 12:15:04.1237  
--  
--(1 row(s) affected)  
```  
  
### <a name="converting-string-literals-to-timen"></a>將字串常值轉換為 time(n)  
 如果整個字串皆是有效的格式，即可從字串常值轉換為日期與時間類型。 否則，就會引發執行階段錯誤。 從日期與時間類型轉換為字串常值的明確轉換不會指定樣式的隱含轉換，一律會採用目前工作階段的預設格式。 下表是字串常值轉換為 **time** 資料類型的規則。  
  
|輸入字串常值|轉換規則|  
|--------------------------|---------------------|  
|ODBC DATE|ODBC 字串常值會對應到 **datetime** 資料類型。 任何將 ODBC DATETIME 常值指派成 **time** 類型的作業，皆會根據轉換規則，執行 **datetime** 與此類型之間的隱含轉換。|  
|ODBC TIME|請參閱上述 ODBC DATE 規則。|  
|ODBC DATETIME|請參閱上述 ODBC DATE 規則。|  
|僅限 DATE|提供預設值。|  
|僅限 TIME|一般|  
|僅限 TIMEZONE|提供預設值。|  
|DATE + TIME|使用輸入字串的 TIME 部分。|  
|DATE + TIMEZONE|不允許。|  
|TIME + TIMEZONE|使用輸入字串的 TIME 部分。|  
|DATE + TIME + TIMEZONE|將使用本機 DATETIME 的 TIME 部分。|  
  
## <a name="examples"></a>範例  
  
### <a name="a-comparing-date-and-time-data-types"></a>A. 比較 date 和 time 資料類型  
 下列範例會比較將字串轉換成各種 **date** 和 **time** 資料類型的結果。  
  
```  
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
  
|資料類型|輸出|  
|---------------|------------|  
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
###  <a name="ExampleB"></a> B. 將有效的時間字串常值插入 time(7) 資料行  
 下表將列出可插入 **time(7)** 資料類型之資料行的不同字串常值，以及之後儲存在該資料行中的值。  
  
|字串常值格式類型|插入的字串常值|儲存的 time(7) 值|Description|  
|--------------------------------|-----------------------------|------------------------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01:123AM'|01:01:01.1230000|當冒號 (:) 出現在小數秒數有效位數之前時，小數位數就無法超過三個位置，否則將會引發錯誤。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 AM'|01:01:01.1234567|指定為 AM 或 PM 時，時間就會採用 24 小時格式儲存，但不含常值 AM 或 PM。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567 PM'|13:01:01.1234567|指定為 AM 或 PM 時，時間就會採用 24 小時格式儲存，但不含常值 AM 或 PM。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01.1234567PM'|13:01:01.1234567|AM 或 PM 之前的空格是選擇性的。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01AM'|01:00:00.0000000|如果只有指定小時，則所有其他值都是 0。|  
|[SQL Server]|'01 AM'|01:00:00.0000000|AM 或 PM 之前的空格是選擇性的。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|'01:01:01'|01:01:01.0000000|沒有指定小數秒數有效位數時，資料類型所定義的每個位置都是 0。|  
|ISO 8601|'01:01:01.1234567'|01:01:01.1234567|若要符合 ISO 8601，請使用 24 小時格式，而非 AM 或 PM。|  
|ISO 8601|'01:01:01.1234567 +01:01'|01:01:01.1234567|雖然輸入中允許使用選擇性的時區差異 (TZD)，但是不會進行儲存。|  
  
### <a name="c-inserting-time-string-literal-into-columns-of-each-date-and-time-date-type"></a>C. 將時間字串常值插入每個 date 和 time 資料類型的資料行  
 在下表中，第一個資料行會顯示即將插入 date 或 time 資料類型 (顯示於第二個資料行) 之資料庫資料表資料行的時間字串常值。 第三個資料行會顯示將儲存在資料庫資料表資料行中的值。  
  
|插入的字串常值|資料行資料類型|儲存在資料行中的值|Description|  
|-----------------------------|----------------------|------------------------------------|-----------------|  
|'12:12:12.1234567'|**time(7)**|12:12:12.1234567|如果小數秒數有效位數超過針對資料行所指定的值，字串就會被截斷，但不會發生錯誤。|  
|'2007-05-07'|**date**|NULL|任何時間值都會導致 INSERT 陳述式失敗。|  
|'12:12:12'|**smalldatetime**|1900-01-01 12:12:00|任何小數秒數有效位數值都會導致 INSERT 陳述式失敗。|  
|'12:12:12.123'|**datetime**|1900-01-01 12:12:12.123|任何長度超過三個位置的秒數有效位數都會導致 INSERT 陳述式失敗。|  
|'12:12:12.1234567'|**datetime2(7)**|1900-01-01 12:12:12.1234567|如果小數秒數有效位數超過針對資料行所指定的值，字串就會被截斷，但不會發生錯誤。|  
|'12:12:12.1234567'|**datetimeoffset(7)**|1900-01-01 12:12:12.1234567 +00:00|如果小數秒數有效位數超過針對資料行所指定的值，字串就會被截斷，但不會發生錯誤。|  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
