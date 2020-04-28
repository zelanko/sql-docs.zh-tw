---
title: 類型支援，ODBC 日期和時間
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], data type support
- ODBC, date/time improvements
ms.assetid: 8e0d9ba2-3ec1-4680-86e3-b2590ba8e2e9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b34d6864bf6b6c36404770f0ab795634dd746dc8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301750"
---
# <a name="data-type-support-for-odbc-date-and-time-improvements"></a>資料類型對 ODBC 日期和時間支援的改善
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題提供有關支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期和時間資料類型之 ODBC 類型的資訊。  
  
## <a name="data-type-mapping-in-parameters-and-resultsets"></a>參數和資料列集中的資料類型對應  
 除了 ODBC 資料類型 (SQL_TYPE_TIMESTAMP 和 SQL_TIMESTAMP) 之外，我們在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 中加入了兩個新的資料類型，以便公開新的伺服器類型：  
  
-   SQL_SS_TIME2  
  
-   SQL_SS_TIMESTAMPOFFSET  
  
 下表顯示完整伺服器類型的對應。 請注意，資料表的某些資料格包含兩個項目：在這些情況下，第一個是 ODBC 3.0 值，而第二個是 ODBC 2.0 值。  
  
|SQL Server 資料類型|SQL 資料類型|值|  
|--------------------------|-------------------|-----------|  
|Datetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
|Date|SQL_TYPE_DATE<br /><br /> SQL_DATE|91（sql .h）<br /><br /> 9（sqlext.h .h）|  
|時間|SQL_SS_TIME2|-154 （SQLNCLI .h）|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|-155 (SQLNCLI.h)|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
||||

 下表列出對應的結構和 ODBC C 類型。 ODBC 不允許使用定義 C 類型的驅動程式，因此，SQL_C_BINARY 會當做二進位結構，用於 time 和 datetimeoffset。  
  
|SQL 資料類型|記憶體配置|預設 C 資料類型|值 (sqlext.h)|  
|-------------------|-------------------|-------------------------|------------------------|  
|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|SQL_TIMESTAMP_STRUCT<br /><br /> TIMESTAMP_STRUCT|SQL_C_TYPE_TIMESTAMP<br /><br /> SQL_C_TIMESTAMP|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|  
|SQL_TYPE_DATE<br /><br /> SQL_DATE|SQL_DATE_STRUCT<br /><br /> DATE_STRUCT|SQL_C_TYPE_DATE<br /><br /> SQL_C_DATE|SQL_TYPE_DATE<br /><br /> SQL_DATE|  
|SQL_SS_TIME2|SQL_SS_TIME2_STRUCT|SQL_C_SS_TIME2<br /><br /> SQL_C_BINARY (ODBC 3.5 和舊版)|0x4000 (sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
|SQL_SS_TIMESTAMPOFFSET|SQL_SS_TIMESTAMPOFFSET_STRUCT|SQL_C_SS_TIMESTAMPOFFSET<br /><br /> SQL_C_BINARY (ODBC 3.5 和舊版)|0x4001 (sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
|||||

 指定 SQL_C_BINARY 繫結時，將會執行對齊檢查，並回報對齊不正確的錯誤。 此錯誤的 SQLSTATE 將為 IM016，其中包含「結構對齊錯誤」訊息。  
  
## <a name="data-formats-strings-and-literals"></a>資料格式：字串和常值  
 下表顯示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型、ODBC 資料類型與 ODBC 字串常值之間的對應。  
  
|SQL Server 資料類型|ODBC 資料類型|用於用戶端轉換的字串格式|  
|--------------------------|--------------------|------------------------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'yyyy-mm-dd hh:mm:ss[.999]'<br /><br /> 針對 Datetime，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最多支援三個小數秒位數。|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'yyyy-mm-dd hh:hh:ss'<br /><br /> 此資料類型的精確度為一分鐘。 輸出時，秒數元件為零，而在輸入時，將會由伺服器捨去。|  
|Date|SQL_TYPE_DATE<br /><br /> SQL_DATE|'yyyy-mm-dd'|  
|時間|SQL_SS_TIME2|'hh:mm:ss[.9999999]'<br /><br /> 您最多可以使用七位數選擇性地指定小數秒。|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|' yyyy-mm-dd hh： mm： ss [. 9999999] '<br /><br /> 您最多可以使用七位數選擇性地指定小數秒。|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|'yyyy-mm-dd hh:mm:ss[.9999999] +/- hh:mm'<br /><br /> 您最多可以使用七位數選擇性地指定小數秒。|  
||||

 日期/時間常值的 ODBC 逸出序列沒有變更。  
  
 結果中的小數秒一律使用點 (.) 而非冒號 (:)。  
  
 傳回到應用程式的字串值一律為適用於給定資料行的相同長度。 年、月、日、十、分和秒元件會以前置零填補以符合最大寬度，而且在 datetime 值的日期和時間之間會有一個空格。 在 datetimeoffset 值的時間和時區位移之間也有一個空格。 時區位移一律置於一個符號之後；當位移為零時，此符號為加號 (+)。 如果需要，小數秒會以尾端零填補，最多填補到針對資料行定義的有效位數。 對於 datetime 資料行，有三個小數秒位數。 對於 smalldatetime 資料行，則沒有小數秒的位數，而且秒數將永遠為零。  
  
 空字串不是有效的日期/時間常值，而且它不代表 NULL 值。 嘗試將空字串轉換為日期/時間值時，將會導致 SQLState 22018 錯誤，而且會出現「轉換規格的字元值無效」訊息。  
  
 從字串參數進行轉換時，字串格式應該相同，但是小時和分鐘為零的時區符號可以是加號或減號，而且小數秒可以使用最多 9 位數的尾端零。 時間元件可以利用一個小數點 (沒有小數秒位數) 結束。  
  
 驅動程式目前在標點符號字元周圍允許額外的空白，而時間和時區位移之間的空格則是選擇性的。 不過，這在後續的版本中可能會有變更；應用程式不應該依賴目前的行為。  
  
## <a name="data-formats-data-structures"></a>資料格式：資料結構  
 在以下描述的結構中，ODBC 會指定採用自西曆的下列條件約束：  
  
-   月份的範圍由 1 至 12。  
  
-   日期欄位範圍為 1 至該月份的天數，而且如果是潤年，則必須與年和月欄位一致。  
  
-   小時的範圍由 0 至 23。  
  
-   分鐘的範圍由 0 至 59。  
  
-   秒數的範圍由 0 至 61.9(n)。 這可讓最多兩個潤秒與恆星時間保持同步。  
  
     請注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許使用潤秒，因此，大於 59 的秒數值將會導致伺服器錯誤。  
  
 下列現有 ODBC 結構的實作已經經過修改，支援新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期和時間資料類型。 不過，定義尚未變更。  
  
-   DATE_STRUCT  
  
-   TIME_STRUCT  
  
-   TIMESTAMP_STRUCT  
  
 另外還有兩個新的結構：  
  
-   SQL_SS_TIME2_STRUCT  
  
-   SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
### <a name="sql_ss_time2_struct"></a>SQL_SS_TIME2_STRUCT  
 此結構在 32 位元和 64 位元作業系統上會填補到 12 個位元組。  
  
```cpp
typedef struct tagSS_TIME2_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
} SQL_SS_TIME2_STRUCT;  
```  
  
### <a name="sql_ss_timestampoffset_struct"></a>SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
```cpp
typedef struct tagSS_TIMESTAMPOFFSET_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
   SQLSMALLINT timezone_hour;  
   SQLSMALLINT timezone_minute;  
} SQL_SS_TIMESTAMPOFFSET_STRUCT;  
```  
  
 如果**timezone_hour**為負數，則**timezone_minute**必須為負數或零。 如果**timezone_hour**為正數，則**timezone_minute**必須為正數或零。 如果**timezone_hour**為零，則**timezone_minute**的範圍可以是-59 到 + 59 之間的任何值。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC&#41;&#40;的日期和時間改善](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
