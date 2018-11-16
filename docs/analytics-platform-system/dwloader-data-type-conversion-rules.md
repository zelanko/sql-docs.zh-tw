---
title: Dwloader 的資料類型轉換規則-Parallel Data Warehouse |Microsoft Docs
description: 本主題描述的輸入的資料格式和隱含資料類型轉換成 Parallel Data Warehouse (PDW) 載入資料時，命令列載入器支援該 dwloader。 」
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1553c02c7d7ff7c1095d4c7217bc628339168a77
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703976"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>資料類型轉換規則 dwloader-平行處理資料倉儲
本主題描述的輸入的資料格式和隱含資料類型轉換的[dwloader 命令列載入器](dwloader.md)時它會將資料載入 PDW 支援。 輸入的資料不符合 SQL Server PDW 目標資料表中的資料類型時，就會發生隱含資料轉換。 設計您的載入程序，以確保您的資料將可順利載入至 SQL Server PDW 時，請使用此資訊。  
   
  
## <a name="InsertBinaryTypes"></a>將常值插入二進位型別  
下表定義可接受的常值類型、 格式和載入類型的 SQL Server PDW 資料行中的常值的轉換規則**二進位**(*n*) 或**varbinary**(*n*)。  
  
|輸入的資料類型|輸入的資料範例|轉換成 binary 或 varbinary 資料類型|  
|-------------------|-----------------------|-----------------------------------------------|  
|二進位常值|[0x]*hexidecimal_string*<br /><br />範例： 12Ef 或 0x12Ef|0x 前置詞是選擇性的。<br /><br />資料來源的長度不能超過指定的資料類型的位元組數目。<br /><br />如果資料來源長度的大小少於**二進位**資料類型，就會進行填補右側以零觸達的資料類型大小。|  
  
## <a name="InsertDateTimeTypes"></a>插入日期和時間類型的常值  
日期和時間常值會以單引號括住的特定格式中使用字串常值。 下表定義允許的常值類型、 格式和載入類型的資料行中的日期或時間常值的轉換規則**datetime**， **smalldatetime**，**日期**，**時間**， **datetimeoffset**，或**datetime2**。 資料表定義指定的資料類型的預設格式。 您可以指定其他格式均定義一節[日期時間格式](#DateFormats)。 日期和時間常值不能包含開頭或尾端空格。 **日期**， **smalldatetime**，且無法載入 null 值，以固定的寬度的模式。  
  
### <a name="datetime-data-type"></a>datetime 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**datetime**。 空字串 （"） 轉換的預設值為 ' 1900年-01-01 12:00:00.000'。 字串，包含只有空白 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|轉換成日期時間資料類型|  
|-------------------|-----------------------|------------------------------------|  
|字串常值**datetime**格式|' yyyy-mm-dd 的-ss [.fff]'<br /><br />範例: ' 2007年-05-08 12:35:29.123'|插入值時，遺失的小數位數會設定為 0。 例如，常值 '2007年-05-08 12:35' 會插入做為 ' 2007年-05-08 12:35:00.000'。|  
|字串常值**smalldatetime**格式|' yyyy 為 yyyy-mm-dd hh: mm '<br /><br />範例: ' 2007年-05-08 12:35 '|秒數和剩餘的小數位數會設定為 0 時則會插入值。|  
|字串常值**日期**格式|'-yyyy-mm-dd '<br /><br />範例: ' 2007年-05-08'|時間值 （小時、 分鐘、 秒和分數） 會設為 12:00:00.000 時則會插入值。|  
|字串常值**datetime2**格式|' yyyy-mm-dd/MM: ss.fffffff '<br /><br />範例: ' 2007年-05-08 12:35:29.1234567'|來源資料不能超過三個小數位數。 例如，常值 '2007年-05-08 12:35:29.123' 將會插入，但值' 2007年-05-8 12:35:29.1234567' 會產生錯誤。|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**smalldatetime**。 空字串 （"） 轉換的預設值為 ' 1900年-01-01 12:00 '。 字串，包含只有空白 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|轉換成 smalldatetime 資料類型|  
|-------------------|-----------------------|-----------------------------------------|  
|字串常值**smalldatetime**格式|'yyyy 為 yyyy-mm-dd hh: mm' 或者 'yyyy 為 yyyy-mm-dd hh: mm:'<br /><br />範例: '2007年-05-08 12:00' 或 ' 2007年-05-08 12:00:15 '|來源資料必須具有值的年份、 月份、 日期、 小時和分鐘。 秒數是選擇性，而且如果有的話，必須設定為 00 的值。 任何其他值會產生錯誤。<br /><br />秒數是選擇性的。 載入時 smalldatetime 資料行，dwloader 會捨入秒和小數秒數。 例如，1999年-01-05 20:10:35.123 會載入為 01 05 20:11。|  
|字串常值**日期**格式|'-yyyy-mm-dd '<br /><br />範例: ' 2007年-05-08'|時間值 （小時、 分鐘、 秒和分數） 會設定為 0，則會插入值時。|  
  
### <a name="date-data-type"></a>日期資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**日期**。 空字串 （"） 轉換的預設值為 ' 1900年-01-01'。 字串，包含只有空白 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|轉換成 date 資料類型|  
|-------------------|-----------------------|--------------------------------|  
|字串常值**日期**格式|'-yyyy-mm-dd '<br /><br />範例: ' 2007年-05-08'||  
  
### <a name="time-data-type"></a>時間資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**時間**。 空字串 （"） 會轉換成預設值 '00:00:00.0000'。 字串，包含只有空白 (' ') 會產生錯誤。  
  
|輸入的資料類型|輸入的資料範例|時間資料類型轉換|  
|-------------------|-----------------------|--------------------------------|  
|字串常值**時間**格式|'hh:mm:ss.fffffff'<br /><br />範例: ' 12:35:29.1234567'|如果資料來源具有小於或等於有效位數 （小數位數） 的有效位數比**時間**資料類型，資料會填補到右邊的零。 例如，常值 '12:35:29.123' 插入為 '12:35:29.1230000'。|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**datetimeoffset** (*n*)。 預設的格式是 ' yyyy-mm-dd/MM: ss.fffffff {+ |-} hh: mm '。 空字串 （"） 轉換的預設值為 ' 1900年-01-01 12:00:00.0000000 + 00:00 '。 字串，包含只有空白 (' ') 會產生錯誤。 小數位數的數目取決於資料行定義。 例如，定義為資料行**datetimeoffset** (2) 將會有兩個小數位數。  
  
|輸入的資料類型|輸入的資料範例|轉換成 datetimeoffset 資料類型|  
|-------------------|-----------------------|------------------------------------------|  
|字串常值**datetime**格式|' yyyy-mm-dd 的-ss [.fff]'<br /><br />範例: ' 2007年-05-08 12:35:29.123'|遺漏的小數位數和位移的值會設定為 0 時則會插入值。 例如，常值 '2007年-05-08 12:35:29.123' 會插入做為' 2007年-05-08 12:35:29.1230000 + 00:00 '。|  
|字串常值**smalldatetime**格式|' yyyy 為 yyyy-mm-dd hh: mm '<br /><br />範例: ' 2007年-05-08 12:35 '|秒數、 剩餘的小數位數和位移的值會設定為 0 時則會插入值。|  
|字串常值**日期**格式|'-yyyy-mm-dd '<br /><br />範例: ' 2007年-05-08'|時間值 （小時、 分鐘、 秒和分數） 會設定為 0，則會插入值時。 例如，常值 '2007年-05-08' 會插入做為' 2007年-05-08 00:00:00.0000000 + 00:00 '。|  
|字串常值**datetime2**格式|' yyyy-mm-dd/MM: ss.fffffff '<br /><br />範例: ' 2007年-05-08 12:35:29.1234567'|來源資料不能超過指定的 datetimeoffset 資料行中的小數秒數。 如果資料來源有小於或等於的小數秒數，就會進行填補右側以零。 比方說，如果資料類型為 datetimeoffset (5)，常值 '2007年-05-08 12:35:29.123 + 12:15' 會插入做為 ' 12:35:29.12300 + 12:15 '。|  
|字串常值**datetimeoffset**格式|' yyyy-mm-dd/MM: ss.fffffff {+&#124;-} hh: mm '<br /><br />範例: ' 2007年-05-08 12:35:29.1234567 + 12:15 '|來源資料不能超過指定的 datetimeoffset 資料行中的小數秒數。 如果資料來源有小於或等於的小數秒數，就會進行填補右側以零。 比方說，如果資料類型為 datetimeoffset (5)，常值 '2007年-05-08 12:35:29.123 + 12:15' 會插入做為 ' 12:35:29.12300 + 12:15 '。|  
  
### <a name="datetime2-data-type"></a>datetime2 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**datetime2** (*n*)。 預設格式為 ' yyyy-mm-dd/MM: ss.fffffff'。 空字串 （"） 轉換的預設值為 ' 1900年-01-01 12:00:00 '。 字串，包含只有空白 (' ') 會產生錯誤。 小數位數的數目取決於資料行定義。 例如，定義為資料行**datetime2** (2) 將會有兩個小數位數。  
  
|輸入的資料類型|輸入的資料範例|轉換成 datetime2 資料類型|  
|-------------------|-----------------------|-------------------------------------|  
|字串常值**datetime**格式|' yyyy-mm-dd 的-ss [.fff]'<br /><br />範例: ' 2007年-05-08 12:35:29.123'|小數秒數是選擇性的則會插入值時，會設定為 0。|  
|字串常值**smalldatetime**格式|' yyyy 為 yyyy-mm-dd hh: mm '<br /><br />範例: ' 2007年-05-08 12'|選擇性的秒數和剩餘的小數位數會設定為 0 時則會插入值。|  
|字串常值**日期**格式|'-yyyy-mm-dd '<br /><br />範例: ' 2007年-05-08'|時間值 （小時、 分鐘、 秒和分數） 會設定為 0，則會插入值時。 例如，常值 '2007年-05-08' 會插入做為' 2007年-05-08 12:00:00.0000000'。|  
|字串常值**datetime2**格式|' yyyy-mm-dd 的-hh:mm:ss:fffffff'<br /><br />範例: ' 2007年-05-08 12:35:29.1234567'|如果資料來源包含日期和時間會小於或等於指定值的元件**datetime2**(*n*)，將資料插入; 否則會產生錯誤。|  
  
### <a name="DateFormats"></a>日期時間格式  
Dwloader 會支援下列資料格式，它會載入到 SQL Server PDW 的輸入資料。 表格後面列出更多詳細資料。  
  
|DATETIME|smalldatetime|日期|datetime2|datetimeoffset|  
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
  
-   若要分隔月、 日和年的值，您可以使用 '-'，'/' 或 '。 '. 為了簡單起見，此表格只使用 ' – ' 分隔符號。  
  
-   若要指定的文字，表示月份會使用三個或多個字元。 月的 1 或 2 個字元會解譯為數字。  
  
-   若要分隔時間值，請使用 ': ' 符號。  
  
-   括在方括號中的字母是選擇性的。  
  
-   字母 'tt' 會指定 [AM|PM|am|pm]。 預設值是 AM。 指定 'tt' 時，小時值 (hh) 的範圍必須介於 0 到 12 之間。  
  
-   字母 'zzz' 會以 {+|-}HH:ss] 格式，指定系統目前時區的時區差距。  
  
## <a name="InsertNumerictypes"></a>將常值插入數字類型  
下表定義載入會使用數值類型的 SQL Server PDW 資料行中的常值的預設格式和轉換規則。  
  
### <a name="bit-data-type"></a>bit 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**元**。 空字串 （"） 或字串，包含只有空白 (' ') 轉換成 0。  
  
|輸入的資料類型|輸入的資料範例|轉換成 bit 資料類型|  
|-------------------|-----------------------|-------------------------------|  
|字串常值**整數**格式|' ffffffffff'<br /><br />範例: '1' 或者 '而 321'|格式化為字串常值的整數值不能包含負數值。 例如，'-123' 的值會產生錯誤。<br /><br />大於 1 的值會轉換成 1。 例如，'123' 的值會轉換成 1。|  
|字串常值|'TRUE' 或者 'FALSE'<br /><br />範例: '，則為 true'|值 'TRUE' 會轉換為 1。值 'FALSE' 會轉換成 0。|  
|整數常值|fffffffn<br /><br />範例： 1 或而 321|大於 1 或小於 0 的值會轉換成 1。 比方說，123 和-123 的值會轉換為 1。|  
|十進位常值|fffnn.fffn<br /><br />範例： 1234.5678|大於 1 或小於 0 的值會轉換成 1。 例如 123.45 和-123.45 值會轉換為 1。|  
  
### <a name="decimal-data-type"></a>Decimal 資料類型  
下表定義載入類型的資料行中的常值的規則**十進位**(*p，s*)。 資料轉換規則會與 SQL Server 相同。 如需詳細資訊，請參閱 <<c0> [ 資料類型轉換 (Database Engine)](https://go.microsoft.com/fwlink/?LinkId=202128) MSDN 上。  
  
|輸入的資料類型|輸入的資料範例|  
|-------------------|-----------------------|  
|整數常值|321312313123|  
|十進位常值|123344.34455|  
  
### <a name="float-and-real-data-types"></a>float 和 real 資料類型  
下表定義載入類型的資料行中的常值的規則**浮點數**或是**實際**。 資料轉換規則會與 SQL Server 相同。 如需詳細資訊，請參閱 <<c0> [ 資料類型轉換 (Database Engine)](../t-sql/data-types/data-type-conversion-database-engine.md) MSDN 上。  
  
|輸入的資料類型|輸入的資料範例|  
|-------------------|-----------------------|  
|整數常值|321312313123|  
|十進位常值|123344.34455|  
|浮動點常值|3.12323E+14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int、 bigint、 tinyint、 smallint 資料類型  
下表定義載入類型的資料行中的常值的規則**int**， **bigint**， **tinyint**，或**smallint**。 資料來源不能超過指定的資料類型所允許的範圍。 例如，針對範圍**tinyint**是 0 到 255 和範圍**int**是-2,147,483,648 到 2,147,483,647。  
  
|輸入的資料類型|輸入的資料範例|轉換為整數資料類型|  
|-------------------|-----------------------|------------------------------------|  
|整數常值|321312313123||  
|十進位常值|123344.34455|要在小數點右邊的值會被截斷。|  
  
### <a name="money-and-smallmoney-data-types"></a>money 和 smallmoney 資料類型  
含有選擇性小數點也可選擇附加貨幣符號做為前置詞的數字字串來表示 money 常值。 資料來源不能超過指定的資料類型所允許的範圍。 例如，針對範圍**smallmoney**是-214，748.3648 214,748.3647 和範圍**money**是從-922,337,203,685,477.5808 到 922,337,203,685,477.5807。 下表定義載入類型的資料行中的常值的規則**金錢**或是**smallmoney**。  
  
|輸入的資料類型|輸入的資料範例|轉換至金額或 smallmoney 資料類型|  
|-------------------|-----------------------|-----------------------------------------------|  
|整數常值|321312|插入值時，遺失的數字的小數點後會設定為 0。 例如，常值 12345 會插入為 12345.0000|  
|十進位常值|123344.34455|如果小數點後數字數目超過 4，值將會無條件進位到最接近值。 例如，為 123344.3446 插入值 123344.34455。|  
|Money 常值|$123456.7890|貨幣符號不會插入的值。<br /><br />如果小數點後數字數目超過 4，值將會無條件進位到最接近值。|  
  
## <a name="InsertStringTypes"></a>將常值插入至字串類型  
下表定義載入用於字串類型的 SQL Server PDW 資料行中的常值的預設格式和轉換規則。  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char、 varchar、 nchar 和 nvarchar 資料類型  
下表定義的預設格式和載入類型的資料行中的常值的規則**char**， **varchar**， **nchar**並**nvarchar**. 資料來源的長度不能超過指定的資料類型的大小。 如果資料來源長度的大小少於**char**或是**nchar**資料類型，就會進行填補空格右邊觸達的資料類型大小。  
  
|輸入的資料類型|輸入的資料範例|轉換成字元資料類型|  
|---------------|-------------------|----------------------------------|  
|字串常值|格式: ' 字元字串 '<br /><br />範例: ' abc'| NA |  
|Unicode 字串常值|格式： N'character 字串 '<br /><br />範例： N'abc'| NA |  
|整數常值|格式： ffffffffffn<br /><br />範例： 321312313123| NA |  
|十進位常值|格式： ffffff.fffffff<br /><br />範例： 12344.34455| NA |  
|Money 常值|格式： $ffffff.fffnn<br /><br />範例: $ 123456.99|選擇附加貨幣符號不會插入的值。 若要插入的貨幣符號，插入的字串常值的值。 這會比對載入器，每個常值視為字串常值的格式。<br /><br />不允許使用逗號。<br /><br />如果小數點後數字數目超過 2，值將會無條件進位到最接近值。 例如，為 123.95 插入值 123.946789。<br /><br />使用 CONVERT 函式插入 money 常值時，將允許只有預設樣式 0 （沒有逗號和小數點後的 2 個數字）。|  
  
### <a name="general-remarks"></a>一般備註  
**dwloader**會執行相同的隱含轉換，SMP SQL Server 執行時，但不支援所有的隱含轉換 SMP SQL Server 支援。  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
