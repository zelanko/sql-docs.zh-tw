---
title: Dwloader 資料類型轉換規則
description: 本主題描述在將資料載入至平行處理資料倉儲（PDW）時，dwloader 命令列載入器支援的輸入資料格式和隱含資料類型轉換。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fe5d8790b5adb8477c994d265f458cdb1ceda61a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401184"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Dwloader 的資料類型轉換規則-平行處理資料倉儲
本主題描述在將資料載入至 PDW 時， [Dwloader 命令列載入](dwloader.md)器支援的輸入資料格式和隱含資料類型轉換。 當輸入資料與 SQL Server PDW 目標資料表中的資料類型不相符時，就會發生隱含資料轉換。 設計您的載入程式時，請使用此資訊，以確保您的資料成功載入 SQL Server PDW。  
   
  
## <a name="inserting-literals-into-binary-types"></a><a name="InsertBinaryTypes"></a>將常值插入二進位類型  
下表定義接受的常數值型別、格式和轉換規則，用於將常值載入至**binary**類型的 SQL Server PDW 資料行（*n*）或**Varbinary**（*n*）。  
  
|輸入資料類型|輸入資料範例|轉換成 binary 或 Varbinary 資料類型|  
|-------------------|-----------------------|-----------------------------------------------|  
|二進位常值|0x*hexidecimal_string*<br /><br />範例：12Ef 或0x12Ef|0x 前置詞是選擇性的。<br /><br />資料來源長度不能超過為資料類型所指定的位元組數目。<br /><br />如果資料來源長度小於**二進位**資料類型的大小，資料會向右填補，而零會到達資料類型大小。|  
  
## <a name="inserting-literals-into-date-and-time-types"></a><a name="InsertDateTimeTypes"></a>將常值插入日期和時間類型  
日期和時間常值是使用特定格式的字串常值來表示，並以單引號括住。 下表定義允許的常數值型別、格式和轉換規則，用於將日期或時間常值載入至**datetime**、 **Smalldatetime**、 **date**、 **time**、 **datetimeoffset**或**datetime2**類型的資料行。 資料表會定義給定資料類型的預設格式。 可以指定的其他格式定義于[Datetime 格式](#DateFormats)一節中。 日期和時間常值不能包含開頭或尾端空格。 不能在固定寬度模式中載入**date**、 **Smalldatetime**和 null 值。  
  
### <a name="datetime-data-type"></a>datetime 資料類型  
下表定義預設的格式，以及將常值載入至**datetime**類型之資料行的規則。 空字串（' '）會轉換成預設值 ' 1900-01-01 12：00： 00.000 '。 只包含空格（' '）的字串會產生錯誤。  
  
|輸入資料類型|輸入資料範例|轉換成 datetime 資料類型|  
|-------------------|-----------------------|------------------------------------|  
|**日期時間**格式的字串常值|' yyyy-mm-dd hh： MM： ss [. fff] '<br /><br />範例： ' 2007-05-08 12：35： 29.123 '|插入值時，遺失的小數位數會設定為0。 例如，常值 ' 2007-05-08 12:35 ' 會插入為 ' 2007-05-08 12：35： 00.000 '。|  
|**Smalldatetime**格式的字串常值|' yyyy-mm-dd hh： MM '<br /><br />範例： ' 2007-05-08 12:35 '|插入值時，秒數和剩餘小數數位會設定為0。|  
|**日期**格式的字串常值|' yyyy-mm-dd '<br /><br />範例： ' 2007-05-08 '|插入值時，時間值（小時、分鐘、秒和分數）會設定為12：00：00.000。|  
|**Datetime2**格式的字串常值|' yyyy-MM-dd hh： MM： ss. fffffff '<br /><br />範例： ' 2007-05-08 12：35： 29.1234567 '|來源資料不能超過三個小數位數。 例如，將會插入常值 ' 2007-05-08 12：35： 29.123 '，但值 ' 2007-05-8 12：35： 29.1234567 ' 會產生錯誤。|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 資料類型  
下表定義預設的格式，以及將常值載入至**Smalldatetime**類型之資料行的規則。 空字串（' '）會轉換成預設值 ' 1900-01-01 12:00 '。 只包含空格（' '）的字串會產生錯誤。  
  
|輸入資料類型|輸入資料範例|轉換成 Smalldatetime 資料類型|  
|-------------------|-----------------------|-----------------------------------------|  
|**Smalldatetime**格式的字串常值|' yyyy-mm-dd hh： mm ' 或 ' yyyy-MM-dd hh： mm： ss '<br /><br />範例： ' 2007-05-08 12:00 ' 或 ' 2007-05-08 12:00:15 '|來源資料必須具有 year、month、date、hour 和 minute 的值。 秒是選擇性的，如果存在，則必須設為值00。 任何其他值都會產生錯誤。<br /><br />秒是選擇性的。 載入 Smalldatetime 資料行時，dwloader 將會四捨五入秒和小數秒。 例如，1999-01-05 20：10：35.123 會載入為 01-05 20:11。|  
|**日期**格式的字串常值|' yyyy-mm-dd '<br /><br />範例： ' 2007-05-08 '|插入值時，時間值（小時、分鐘、秒和分數）會設定為0。|  
  
### <a name="date-data-type"></a>日期資料類型  
下表定義預設的格式，以及將常值載入至 date 類型之**資料**行的規則。 空字串（' '）會轉換成預設值 ' 1900-01-01 '。 只包含空格（' '）的字串會產生錯誤。  
  
|輸入資料類型|輸入資料範例|轉換成日期資料類型|  
|-------------------|-----------------------|--------------------------------|  
|**日期**格式的字串常值|' yyyy-mm-dd '<br /><br />範例： ' 2007-05-08 '||  
  
### <a name="time-data-type"></a>time 資料類型  
下表定義預設的格式，以及將常值載入至**time**類型之資料行的規則。 空字串（' '）會轉換成預設值 ' 00：00： 00.0000 '。 只包含空格（' '）的字串會產生錯誤。  
  
|輸入資料類型|輸入資料範例|轉換成 time 資料類型|  
|-------------------|-----------------------|--------------------------------|  
|**時間**格式的字串常值|' hh： mm： ss. fffffff '<br /><br />範例： ' 12：35： 29.1234567 '|如果資料來源的精確度小於或等於**時間**資料類型的有效位數，則資料會以零填補到右邊。 例如，常值 ' 12：35： 29.123 ' 會插入為 ' 12：35： 29.1230000 '。|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 資料類型  
下表定義預設的格式，以及將常值載入至類型**datetimeoffset** （*n*）之資料行的規則。 預設格式為 ' yyyy-MM-dd hh： mm： ss. fffffff {+ |-} hh： mm '。 空字串（' '）會轉換成預設值 ' 1900-01-01 12：00： 00.0000000 + 00:00 '。 只包含空格（' '）的字串會產生錯誤。 小數數位的數目取決於資料行定義。 例如，定義為**datetimeoffset** （2）的資料行將會有兩個小數位數。  
  
|輸入資料類型|輸入資料範例|轉換成 datetimeoffset 資料類型|  
|-------------------|-----------------------|------------------------------------------|  
|**日期時間**格式的字串常值|' yyyy-mm-dd hh： MM： ss [. fff] '<br /><br />範例： ' 2007-05-08 12：35： 29.123 '|插入值時，遺失的小數位數和位移值會設為0。 例如，常值 ' 2007-05-08 12：35： 29.123 ' 會插入為 ' 2007-05-08 12：35： 29.1230000 + 00:00 '。|  
|**Smalldatetime**格式的字串常值|' yyyy-mm-dd hh： MM '<br /><br />範例： ' 2007-05-08 12:35 '|秒，插入值時，剩餘的小數位數和位移值都會設定為0。|  
|**日期**格式的字串常值|' yyyy-mm-dd '<br /><br />範例： ' 2007-05-08 '|插入值時，時間值（小時、分鐘、秒和分數）會設定為0。 例如，常值 ' 2007-05-08 ' 會插入為 ' 2007-05-08 00：00： 00.0000000 + 00:00 '。|  
|**Datetime2**格式的字串常值|' yyyy-MM-dd hh： MM： ss. fffffff '<br /><br />範例： ' 2007-05-08 12：35： 29.1234567 '|來源資料不能超過 datetimeoffset 資料行中指定的小數秒數。 如果資料來源的小數秒數較小或相等，資料會向右填補零。 例如，如果資料類型為 datetimeoffset （5），則常值 ' 2007-05-08 12：35： 29.123 + 12:15 ' 會插入為 ' 12：35： 29.12300 + 12:15 '。|  
|**Datetimeoffset**格式的字串常值|' yyyy-mm-dd hh： mm： ss. fffffff {+&#124;-} hh： mm '<br /><br />範例： ' 2007-05-08 12：35： 29.1234567 + 12:15 '|來源資料不能超過 datetimeoffset 資料行中指定的小數秒數。 如果資料來源的小數秒數較小或相等，資料會向右填補零。 例如，如果資料類型為 datetimeoffset （5），則常值 ' 2007-05-08 12：35： 29.123 + 12:15 ' 會插入為 ' 12：35： 29.12300 + 12:15 '。|  
  
### <a name="datetime2-data-type"></a>datetime2 資料類型  
下表定義預設的格式，以及將常值載入**datetime2** （*n*）類型之資料行的規則。 預設格式為 ' yyyy-MM-dd hh： MM： ss. fffffff '。 空字串（' '）會轉換成預設值 ' 1900-01-01 12:00:00 '。 只包含空格（' '）的字串會產生錯誤。 小數數位的數目取決於資料行定義。 例如，定義為**datetime2** （2）的資料行將會有兩個小數位數。  
  
|輸入資料類型|輸入資料範例|轉換成 datetime2 資料類型|  
|-------------------|-----------------------|-------------------------------------|  
|**日期時間**格式的字串常值|' yyyy-mm-dd hh： MM： ss [. fff] '<br /><br />範例： ' 2007-05-08 12：35： 29.123 '|小數秒是選擇性的，而且會在插入值時設定為0。|  
|**Smalldatetime**格式的字串常值|' yyyy-mm-dd hh： MM '<br /><br />範例： ' 2007-05-08 12 '|插入值時，選擇性的秒數和剩餘的小數數位都會設定為0。|  
|**日期**格式的字串常值|' yyyy-mm-dd '<br /><br />範例： ' 2007-05-08 '|插入值時，時間值（小時、分鐘、秒和分數）會設定為0。 例如，常值 ' 2007-05-08 ' 會插入為 ' 2007-05-08 12：00： 00.0000000 '。|  
|**Datetime2**格式的字串常值|' yyyy-MM-dd hh： MM： ss： fffffff '<br /><br />範例： ' 2007-05-08 12：35： 29.1234567 '|如果資料來源包含的資料和時間元件小於或等於**datetime2**（*n*）中指定的值，則會插入資料;否則會產生錯誤。|  
  
### <a name="datetime-formats"></a><a name="DateFormats"></a>日期時間格式  
Dwloader 針對載入 SQL Server PDW 的輸入資料，支援下列資料格式。 資料表後面會列出更多詳細資料。  
  
|Datetime|smalldatetime|date|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
詳細資料：  
  
-   若要分隔月、日和年的值，您可以使用 '-'、'/' 或 '。 '. 為了簡單起見，此表格只使用 '-' 分隔符號。  
  
-   若要將月份指定為文字，請使用三個或多個字元。 包含1或2個字元的月份將會被視為數位。  
  
-   若要分隔時間值，請使用 '： ' 符號。  
  
-   括在方括號中的字母是選擇性的。  
  
-   字母 'tt' 會指定 [AM|PM|am|pm]。 預設值是 AM。 指定 'tt' 時，小時值 (hh) 的範圍必須介於 0 到 12 之間。  
  
-   字母 'zzz' 會以 {+|-}HH:ss] 格式，指定系統目前時區的時區差距。  
  
## <a name="inserting-literals-into-numeric-types"></a><a name="InsertNumerictypes"></a>將常值插入數數值型別  
下表定義預設格式和轉換規則，用於將常值載入至使用數數值型別的 SQL Server PDW 資料行。  
  
### <a name="bit-data-type"></a>bit 資料類型  
下表定義預設的格式，以及將常值載入至**bit**類型之資料行的規則。 空字串（' '）或只包含空白（' '）的字串會轉換為0。  
  
|輸入資料類型|輸入資料範例|轉換成 bit 資料類型|  
|-------------------|-----------------------|-------------------------------|  
|**整數**格式的字串常值|'ffffffffff'<br /><br />範例： ' 1 ' 或 ' 321 '|格式化為字串常值的整數值不能包含負值。 例如，值 '-123 ' 會產生錯誤。<br /><br />大於1的值會轉換成1。 例如，值 ' 123 ' 會轉換成1。|  
|字串常值|' TRUE ' 或 ' FALSE '<br /><br />範例： ' true '|值 ' TRUE ' 轉換成 1;值 ' FALSE ' 會轉換為0。|  
|整數常值|fffffffn<br /><br />範例：1或321|大於1或小於0的值會轉換成1。 例如，值123和-123 會轉換成1。|  
|十進位常值|fffnn.fffn<br /><br />範例：1234.5678|大於1或小於0的值會轉換成1。 例如，值123.45 和-123.45 會轉換成1。|  
  
### <a name="decimal-data-type"></a>decimal 資料類型  
下表定義將常值載入**decimal** （*p，s*）類型之資料行的規則。 資料轉換規則與 SQL Server 相同。 如需詳細資訊，請參閱 MSDN 上的[資料類型轉換（資料庫引擎）](https://go.microsoft.com/fwlink/?LinkId=202128) 。  
  
|輸入資料類型|輸入資料範例|  
|-------------------|-----------------------|  
|整數常值|321312313123|  
|十進位常值|123344.34455|  
  
### <a name="float-and-real-data-types"></a>float 和 real 資料類型  
下表定義將常值載入**float**或**real**類型之資料行的規則。 資料轉換規則與 SQL Server 相同。 如需詳細資訊，請參閱 MSDN 上的[資料類型轉換（資料庫引擎）](../t-sql/data-types/data-type-conversion-database-engine.md) 。  
  
|輸入資料類型|輸入資料範例|  
|-------------------|-----------------------|  
|整數常值|321312313123|  
|十進位常值|123344.34455|  
|浮點常值|3.12323 e + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int、Bigint、Tinyint、Smallint 資料類型  
下表定義將常值載入**int**、 **Bigint**、 **Tinyint**或**Smallint**類型之資料行的規則。 資料來源不能超過給定資料類型所允許的範圍。 例如， **Tinyint**的範圍是0到255，而**int**的範圍是-2147483648 到2147483647。  
  
|輸入資料類型|輸入資料範例|轉換成整數資料類型|  
|-------------------|-----------------------|------------------------------------|  
|整數常值|321312313123||  
|十進位常值|123344.34455|小數點右邊的值會被截斷。|  
  
### <a name="money-and-smallmoney-data-types"></a>money 和 smallmoney 資料類型  
Money 常值是以數位字串表示，其中包含選擇性的小數點和選擇性的貨幣符號做為前置詞。 資料來源不能超過給定資料類型所允許的範圍。 例如， **smallmoney**的範圍是-214748.3648 到214748.3647，而**money**的範圍是-922337203685477.5808 到922337203685477.5807。 下表定義將常值載入**money**或**smallmoney**類型之資料行的規則。  
  
|輸入資料類型|輸入資料範例|轉換成 money 或 smallmoney 資料類型|  
|-------------------|-----------------------|-----------------------------------------------|  
|整數常值|321312|當插入值時，小數點之後遺失的數位會設定為0。 例如，常值12345會插入為12345.0000|  
|十進位常值|123344.34455|如果小數點後的位數超過4，此值會無條件進位到最接近的值。 例如，值123344.34455 會插入為123344.3446。|  
|Money 常值|$123456.7890|不會使用值插入貨幣符號。<br /><br />如果小數點後的位數超過4，此值會無條件進位到最接近的值。|  
  
## <a name="inserting-literals-into-string-types"></a><a name="InsertStringTypes"></a>將常值插入字串類型  
下表定義預設格式和轉換規則，用於將常值載入至使用字串類型的 SQL Server PDW 資料行。  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char、Varchar、Nchar 和 Nvarchar 資料類型  
下表定義預設的格式，以及將常值載入**char**、 **Varchar**、 **Nchar**和**Nvarchar**類型之資料行的規則。 資料來源長度不能超過針對資料類型所指定的大小。 如果資料來源長度小於**char**或**Nchar**資料類型的大小，資料就會以空格填補至右邊，以達到資料類型大小。  
  
|輸入資料類型|輸入資料範例|轉換成字元資料類型|  
|---------------|-------------------|----------------------------------|  
|字串常值|格式： ' 字元字串 '<br /><br />範例： ' abc '| NA |  
|Unicode 字串常值|格式： N'character 字串 '<br /><br />範例： N'abc '| NA |  
|整數常值|格式： ffffffffffn<br /><br />範例：321312313123| NA |  
|十進位常值|格式： ffffff. fffffff<br /><br />範例：12344.34455| NA |  
|Money 常值|格式： $ffffff. fffnn<br /><br />範例： $123456.99|選擇性貨幣符號不會插入值。 若要插入貨幣符號，請將值插入為字串常值。 這會符合載入器的格式，其會將每個常值視為字串常值。<br /><br />不允許使用逗號。<br /><br />如果小數點後的位數超過2，此值會無條件進位到最接近的值。 例如，值123.946789 會插入為123.95。<br /><br />使用 CONVERT 函式插入 money 常值時，只允許預設樣式0（小數點後面沒有逗號和2位數）。|  
  
### <a name="general-remarks"></a>一般備註  
**dwloader**會執行 smp SQL Server 執行的相同隱含轉換，但不支援 smp SQL Server 支援的所有隱含轉換。  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
