---
title: "資料類型 dwloader 轉換的規則"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "本主題描述的輸入的資料格式和隱含資料類型轉換時它會將資料載入 PDW 命令列載入器可支援該 dwloader。"
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 79c48520-b08b-4b15-a943-a551cc90a2c4
caps.latest.revision: "30"
ms.openlocfilehash: 29cf43b7bb5ea38d821e62b03cc125fe5e0fc30c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="data-type-conversion-rules-for-dwloader"></a>資料類型 dwloader 轉換的規則
本主題描述的輸入的資料格式和隱含資料類型轉換， [dwloader 命令列載入器](dwloader.md)時它會將資料載入 PDW 支援。 輸入的資料與 SQL Server PDW 目標資料表中的資料類型不相符時，就會發生隱含資料轉換。 設計您的載入程序，以確保您的資料將可順利載入到 SQL Server PDW 時，請使用此資訊。  
   
  
## <a name="InsertBinaryTypes"></a>將常值插入二進位型別  
下表定義可接受的常值類型、 格式和載入類型的 SQL Server PDW 資料行中的常值的轉換規則**二進位**(*n*) 或**varbinary**(*n*)。  
  
|輸入的資料類型|輸入的資料範例|轉換成 binary 或 varbinary 資料類型|  
|-------------------|-----------------------|-----------------------------------------------|  
|二進位常值|[0 x]*hexidecimal_string*<br /><br />範例： 12Ef 或 0x12Ef|0x 前置詞是選擇性的。<br /><br />資料來源的長度不能超過指定的資料類型的位元組數目。<br /><br />如果資料來源的長度小於大小**二進位**資料類型，就會進行填補至資料類型大小加上零右邊。|  
  
## <a name="InsertDateTimeTypes"></a>將常值插入日期和時間類型  
日期和時間常值會以單引號括住的特定格式中使用字串常值。 下表定義允許的常值類型、 格式和載入類型的資料行的日期或時間常值的轉換規則**datetime**， **smalldatetime**，**日期**，**時間**， **datetimeoffset**，或**datetime2**。 資料表定義的指定的資料類型的預設格式。 您可以指定其他格式區段中定義[日期時間格式](#DateFormats)。 日期和時間常值不能包含開頭或尾端空格。 **日期**， **smalldatetime**，並在固定的寬度模式中，無法載入 null 值。  
  
### <a name="datetime-data-type"></a>datetime 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**datetime**。 空字串 （"） 會轉換成預設值 ' 1900年-01-01 12:00:00.000'。 包含僅空白字串 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|轉換成日期時間資料類型|  
|-------------------|-----------------------|------------------------------------|  
|字串常值中**datetime**格式|' yyyy MM dd hh: mm: [.fff]'<br /><br />範例: ' 2007年-05-08 12:35:29.123'|插入值時，遺失的小數點後數字會設為 0。 例如，常值 '2007年-05-08 12:35' 會插入做為 ' 2007年-05-08 12:35:00.000'。|  
|字串常值中**smalldatetime**格式|' yyyy MM dd hh: mm '<br /><br />範例: ' 2007年-05-08 12:35 '|秒和小數的其餘位數時都會設為 0 會插入的值。|  
|字串常值中**日期**格式|' yyyy-MM-dd'<br /><br />範例: ' 2007年-05-08'|時間值 （小時、 分鐘、 秒和分數） 會設定為 12:00:00.000 時插入的值。|  
|字串常值中**datetime2**格式|' yyyy MM dd: ss.fffffff '<br /><br />範例: ' 2007年-05-08 12:35:29.1234567'|來源資料不能超過三個小數的數字。 例如，常值 '2007年-05-08 12:35:29.123' 將會插入，但值' 2007年-05-8 12:35:29.1234567' 會產生錯誤。|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**smalldatetime**。 空字串 （"） 會轉換成預設值 ' 1900年-01-01 12:00 '。 包含僅空白字串 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|轉換成 smalldatetime 資料類型|  
|-------------------|-----------------------|-----------------------------------------|  
|字串常值中**smalldatetime**格式|'yyyy MM dd hh: mm' 或者 'yyyy MM dd hh: mm:'<br /><br />範例: '2007年-05-08 12:00' 或 ' 2007年-05-08 12:00:15 '|來源資料必須具有值的年份、 月份、 日期、 小時和分鐘。 秒數是選擇性，如果有的話，必須設定為 00 的值。 任何其他值會產生錯誤。<br /><br />秒數是選擇性的。 載入時 smalldatetime 資料行，dwloader 會無條件進位秒和小數秒。 例如，1999年-01-05 20:10:35.123 會載入為 01-05 20:11。|  
|字串常值中**日期**格式|' yyyy-MM-dd'<br /><br />範例: ' 2007年-05-08'|時間 （小時、 分鐘、 秒和分數） 時值都會設為 0 會插入的值。|  
  
### <a name="date-data-type"></a>日期資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**日期**。 空字串 （"） 會轉換成預設值 ' 1900年-01-01'。 包含僅空白字串 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|轉換成 date 資料類型|  
|-------------------|-----------------------|--------------------------------|  
|字串常值中**日期**格式|' yyyy-MM-dd'<br /><br />範例: ' 2007年-05-08'||  
  
### <a name="time-data-type"></a>時間資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**時間**。 空字串 （"） 會轉換成預設值 '00:00:00.0000'。 包含僅空白字串 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|時間資料類型的轉換|  
|-------------------|-----------------------|--------------------------------|  
|字串常值中**時間**格式|': ss.fffffff '<br /><br />範例: ' 12:35:29.1234567'|資料來源是否小於或等於有效位數 （小數位數） 的有效位數比**時間**資料類型，就會進行填補零的右邊。 例如，常值 '12:35:29.123' 插入為 '12:35:29.1230000'。|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**datetimeoffset** (*n*)。 預設的格式是 ' yyyy MM dd: ss.fffffff {+ |-} hh: mm '。 空字串 （"） 會轉換成預設值 ' 1900年-01-01 12:00:00.0000000 + 00:00 '。 包含僅空白字串 (' ') 會產生錯誤。 小數位數取決於資料行定義。 例如，資料行定義為**datetimeoffset** (2) 將會有兩個小數。  
  
|輸入的資料類型|輸入的資料範例|轉換成 datetimeoffset 資料類型|  
|-------------------|-----------------------|------------------------------------------|  
|字串常值中**datetime**格式|' yyyy MM dd hh: mm: [.fff]'<br /><br />範例: ' 2007年-05-08 12:35:29.123'|遺失的小數點後數字和位移的值時都會設為 0 會插入的值。 例如，常值 '2007年-05-08 12:35:29.123' 會插入做為' 2007年-05-08 12:35:29.1230000 + 00:00 '。|  
|字串常值中**smalldatetime**格式|' yyyy MM dd hh: mm '<br /><br />範例: ' 2007年-05-08 12:35 '|秒數、 剩餘的小數點後數字和位移的值時都會設為 0 會插入的值。|  
|字串常值中**日期**格式|' yyyy-MM-dd'<br /><br />範例: ' 2007年-05-08'|時間 （小時、 分鐘、 秒和分數） 時值都會設為 0 會插入的值。 例如，常值 '2007年-05-08' 會插入做為' 2007年-05-08 00:00:00.0000000 + 00:00 '。|  
|字串常值中**datetime2**格式|' yyyy MM dd: ss.fffffff '<br /><br />範例: ' 2007年-05-08 12:35:29.1234567'|來源資料不能超過指定的 datetimeoffset 資料行中的小數秒數。 如果資料來源的小數秒數小於或等於數目，資料右側以零填補。 例如，如果資料類型為 datetimeoffset (5)、 常值 '2007年-05-08 12:35:29.123 + 12:15' 會插入做為 ' 12:35:29.12300 + 12:15 '。|  
|字串常值中**datetimeoffset**格式|' yyyy MM dd: ss.fffffff {+ &#124;-} hh: mm '<br /><br />範例: ' 2007年-05-08 12:35:29.1234567 + 12:15 '|來源資料不能超過指定的 datetimeoffset 資料行中的小數秒數。 如果資料來源的小數秒數小於或等於數目，資料右側以零填補。 例如，如果資料類型為 datetimeoffset (5)、 常值 '2007年-05-08 12:35:29.123 + 12:15' 會插入做為 ' 12:35:29.12300 + 12:15 '。|  
  
### <a name="datetime2-data-type"></a>datetime2 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**datetime2** (*n*)。 預設格式為 'yyyy MM dd: ss.fffffff'。 空字串 （"） 會轉換成預設值 ' 1900年-01-01 12:00:00 '。 包含僅空白字串 (' ') 會產生錯誤。 小數位數取決於資料行定義。 例如，資料行定義為**datetime2** (2) 將會有兩個小數。  
  
|輸入的資料類型|輸入的資料範例|Datetime2 資料類型轉換|  
|-------------------|-----------------------|-------------------------------------|  
|字串常值中**datetime**格式|' yyyy MM dd hh: mm: [.fff]'<br /><br />範例: ' 2007年-05-08 12:35:29.123'|小數秒數是選擇性的則會插入值時，會設定為 0。|  
|字串常值中**smalldatetime**格式|' yyyy MM dd hh: mm '<br /><br />範例: ' 2007年-05-08 12'|選擇性的秒數及剩餘的小數點後數字時都會設為 0 會插入的值。|  
|字串常值中**日期**格式|' yyyy-MM-dd'<br /><br />範例: ' 2007年-05-08'|時間 （小時、 分鐘、 秒和分數） 時值都會設為 0 會插入的值。 例如，常值 '2007年-05-08' 會插入做為' 2007年-05-08 12:00:00.0000000'。|  
|字串常值中**datetime2**格式|' yyyy MM dd hh:mm:ss:fffffff'<br /><br />範例: ' 2007年-05-08 12:35:29.1234567'|如果資料來源包含小於或等於指定的值的日期和時間元件**datetime2**(*n*)，將資料插入; 否則會產生錯誤。|  
  
### <a name="DateFormats"></a>日期時間格式  
Dwloader 輸入資料載入到 SQL Server PDW 支援下列資料格式。 更多詳細資料列在表格之後。  
  
|DATETIME|smalldatetime|日期|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[[M] M]M-[d] d-[yy] yy hh: mm: [.fff]|[[M] M]M-[d] d-[yy] yy hh: mm [: 00]|[[M] M]M-[d] d-[yy] yy|[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff]|[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff] zzz|  
|[[M] M]M-[d] d-[yy] yy hh: mm: [.fff] [tt]|[[M] M]M-[d] d-[yy] yy hh: mm [: 00] [tt]||[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff] [tt]|[[M] M]M-[d] d-[yy] yy hh: mm: [.fffffff] [tt] zzz|  
|[[M] M]M [yy] yy-[d] d hh: mm: [.fff]|[[M] M]M [yy] yy-[d] d hh: mm [: 00]|[[M] M]M [yy] yy-[d] d|[[M] M]M [yy] yy-[d] d hh: mm: [.fffffff]|[[M] M]M [yy] yy-[d] d hh: mm: [.fffffff] zzz|  
|[[M] M]M-[yy] yy-[d] d hh: mm: [.fff] [tt]|[[M] M]M-[yy] yy-[d] d hh: mm [: 00] [tt]||[[M] M]M-[yy] yy-[d] d hh: mm: [.fffffff] [tt]|[[M] M]M-[yy] yy-[d] d hh: mm: [.fffffff] [tt] zzz|  
|[yy] yy-[[M] M] M-[d] d hh: mm: [.fff]|[yy] yy-[[M] M] M-[d] d hh: mm [: 00]|[yy] yy-[[M] M] M-[d] d|[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff]|[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff] zzz|  
|[yy] yy-[[M] M] M-[d] d hh: mm: [.fff] [tt]|[yy] yy-[[M] M] M-[d] d hh: mm [: 00] [tt]||[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff] [tt]|[yy] yy-[[M] M] M-[d] d hh: mm: [.fffffff] [tt] zzz|  
|[yy] yy-[d] d-[[M] M] M hh: mm: [.fff]|[yy] yy-[d] d-[[M] M] M hh: mm [: 00]|[yy] yy-d [d]-[[M] M] M|[yy] yy-[d] d-[[M] M] M hh: mm: [.fffffff]|[yy] yy-[d] d-[[M] M] M ss [.fffffff] zzz|  
|[yy] yy-[d] d-[[M] M] M hh: mm: [.fff] [tt]|[yy] yy-[d] d-[[M] M] M hh: mm [: 00] [tt]||[yy] yy-[d] d-[[M] M] M hh: mm: [.fffffff] [tt]|[yy] yy-[d] d-[[M] M] M hh: mm: [.fffffff] [tt] zzz|  
|[d] d-[[M] M] M-[yy] yy hh: mm: [.fff]|[d] d-[[M] M] M-[yy] yy hh: mm [: 00]|[d] d-[[M] M] M-[yy] yy|[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff]|[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff] zzz|  
|[d] d-[[M] M] M-[yy] yy hh: mm: [.fff] [tt]|[d] d-[[M] M] M-[yy] yy hh: mm [: 00] [tt]||[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff] [tt]|[d] d-[[M] M] M-[yy] yy hh: mm: [.fffffff] [tt] zzz|  
|[d] d-[yy] yy-[[M] M] M hh: mm: [.fff]|[d] d-[yy] yy-[[M] M] M hh: mm [: 00]|[d] d-[yy] yy-[[M] M] M|[d] d-[yy] yy-[[M] M] M hh: mm: [.fffffff]|[d] d-[yy] yy-[[M] M] M ss [.fffffff] zzz|  
|[d] d-[yy] yy-[[M] M] M hh: mm: [.fff] [tt]|[d] d-[yy] yy-[[M] M] M hh: mm [: 00] [tt]||[d] d-[yy] yy-[[M] M] M hh: mm: [.fffffff] [tt]|[d] d-[yy] yy-[[M] M] M hh: mm: [.fffffff] [tt] zzz|  
  
詳細資料：  
  
-   若要分隔月、 日和年值，您可以使用 '-'，'/' 或 '。 '. 為了簡單起見，資料表會使用只在 '-' 分隔符號。  
  
-   若要指定文字，表示月份會使用三個或多個字元。 1 或 2 個字元的月份會解譯為數字。  
  
-   若要分隔時間值，請使用 ': ' 符號。  
  
-   以方括弧括住的字母是選擇性的。  
  
-   字母 'tt' 指定 [AM |PM | am | pm]。 AM 是預設值。 當指定 'tt' 時，小時值 (hh) 必須在 0 到 12 的範圍內。  
  
-   字母 'zzz' 指定系統的目前的時區格式的時區位移 {+ |-} HH:ss]。  
  
## <a name="InsertNumerictypes"></a>將常值插入數值類型  
下表定義的常值載入使用數值類型的 SQL Server PDW 資料行的預設格式和轉換規則。  
  
### <a name="bit-data-type"></a>bit 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**元**。 空字串 （"） 或包含只是空白的字串 (' ') 轉換成 0。  
  
|輸入的資料類型|輸入的資料範例|轉換成 bit 資料類型|  
|-------------------|-----------------------|-------------------------------|  
|字串常值中**整數**格式|' ffffffffff'<br /><br />範例: '1' 或者 '321'|整數值格式化為字串常值不可為負值。 例如，'-123' 的值會產生錯誤。<br /><br />大於 1 的值會轉換成 1。 例如，'123' 的值會轉換成 1。|  
|字串常值|'TRUE' 或者 'FALSE'<br /><br />True 範例: ''|值 'TRUE' 會轉換為 1。'FALSE' 的值會轉換成 0。|  
|整數常值|fffffffn<br /><br />範例： 1 或 321|大於 1 或小於 0 的值會轉換成 1。 例如，123 與-123 這些值會轉換為 1。|  
|十進位常值|fffnn.fffn<br /><br />範例： 1234.5678|大於 1 或小於 0 的值會轉換成 1。 例如 123.45 和-123.45 這些值會轉換為 1。|  
  
### <a name="decimal-data-type"></a>decimal 資料類型  
下表定義載入類型的資料行中的常值的規則**十進位**(*p，s*)。 資料轉換規則是與 SQL Server 相同。 如需詳細資訊，請參閱[資料類型轉換 (Database Engine)](http://go.microsoft.com/fwlink/?LinkId=202128) MSDN 上。  
  
|輸入的資料類型|輸入的資料範例|  
|-------------------|-----------------------|  
|整數常值|321312313123|  
|十進位常值|123344.34455|  
  
### <a name="float-and-real-data-types"></a>float 和 real 資料類型  
下表定義的常值載入類型的資料行規則**float**或**真實**。 資料轉換規則是與 SQL Server 相同。 如需詳細資訊，請參閱[資料類型轉換 (Database Engine)](../t-sql/data-types/data-type-conversion-database-engine.md) MSDN 上。  
  
|輸入的資料類型|輸入的資料範例|  
|-------------------|-----------------------|  
|整數常值|321312313123|  
|十進位常值|123344.34455|  
|浮動點常值|3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int、 bigint、 tinyint、 smallint 資料類型  
下表定義載入類型的資料行中的常值的規則**int**， **bigint**， **tinyint**，或**smallint**。 資料來源不能超過指定的資料類型所允許的範圍。 例如，針對範圍**tinyint**且 0 到 255 的範圍**int**是-2,147,483,648 到 2,147,483,647。  
  
|輸入的資料類型|輸入的資料範例|轉換為整數資料類型|  
|-------------------|-----------------------|------------------------------------|  
|整數常值|321312313123||  
|十進位常值|123344.34455|要在小數點右邊的值會被截斷。|  
  
### <a name="money-and-smallmoney-data-types"></a>money 和 smallmoney 資料類型  
Money 常值會以貨幣符號做為前置詞與可選擇小數點的數字的字串表示。 資料來源不能超過指定的資料類型所允許的範圍。 例如，針對範圍**smallmoney**是-214,748.3648 214,748.3647 和範圍**money**是-922,337,203,685,477.5808 到 922,337,203,685,477.5807。 下表定義載入類型的資料行中的常值的規則**money**或**smallmoney**。  
  
|輸入的資料類型|輸入的資料範例|轉換至 money 或 smallmoney 資料類型|  
|-------------------|-----------------------|-----------------------------------------------|  
|整數常值|321312|插入值時，遺失的數字的小數點後會設定為 0。 例如，常值 12345 會插入成為 12345.0000|  
|十進位常值|123344.34455|如果在小數點之後位數的數目超過 4，值會無條件進位到最接近值。 例如，為 123344.3446 插入值 123344.34455。|  
|Money 常值|$123456.7890|貨幣符號不會插入的值。<br /><br />如果在小數點之後位數的數目超過 4，值會無條件進位到最接近值。|  
  
## <a name="InsertStringTypes"></a>將常值插入字串型別  
下表定義常值載入使用字串類型的 SQL Server PDW 資料行的預設格式和轉換規則。  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char、 varchar、 nchar 和 nvarchar 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**char**， **varchar**， **nchar**和**nvarchar**. 資料來源的長度不能超過指定的資料類型的大小。 如果資料來源的長度小於大小**char**或**nchar**資料類型，就會進行填補空格來取用的資料類型大小的右邊。  
  
|輸入的資料類型|輸入的資料範例|轉換成字元資料類型|  
|---------------|-------------------|----------------------------------|  
|字串常值|格式: ' 字元字串 '<br /><br />範例: ' abc'| NA |  
|Unicode 字串常值|格式： N'character 字串 '<br /><br />範例： N'abc'| NA |  
|整數常值|格式： ffffffffffn<br /><br />範例： 321312313123| NA |  
|十進位常值|格式： ffffff.fffffff<br /><br />範例： 12344.34455| NA |  
|Money 常值|格式： $ffffff.fffnn<br /><br />範例: $ 123456.99|選擇附加貨幣符號不會插入的值。 若要插入的貨幣符號，插入的值為字串常值。 這會比對載入器，每個常值視為字串常值的格式。<br /><br />不允許使用逗號。<br /><br />如果在小數點之後位數的數目超過 2，值會無條件進位到最接近值。 例如，為 123.95 插入值 123.946789。<br /><br />要插入 money 常值使用 CONVERT 函數時，將允許只有預設樣式 0 （沒有逗號和小數點後的 2 位數）。|  
  
### <a name="general-remarks"></a>一般備註  
**dwloader**執行相同的隱含轉換 SMP SQL Server 執行，但不支援所有的隱含轉換 SMP SQL Server 支援的。  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
