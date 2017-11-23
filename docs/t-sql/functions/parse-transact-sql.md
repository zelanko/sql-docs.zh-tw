---
title: "剖析 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PARSE
- PARSE_TSQL
dev_langs: TSQL
helpviewer_keywords: PARSE function
ms.assetid: 6a2dbf10-f692-471b-9458-24d246963049
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 3e172a7d68edc212ce4803103dc1f975e4bf89db
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="parse-transact-sql"></a>PARSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回轉譯成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中所要求資料類型的運算式結果。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
PARSE ( string_value AS data_type [ USING culture ] )  
```  
  
## <a name="arguments"></a>引數  
 *string_value*  
 **nvarchar**(4000) 值，代表要剖析為指定的資料類型的格式化的值。  
  
 *string_value*必須是有效的表示法之要求的資料類型的 PARSE 會引發錯誤。  
  
 *data_type*  
 表示結果之資料類型的常值。  
  
 *文化特性*  
 識別在其中的文化特性的選擇性字串*string_value*格式化。  
  
 如果*文化特性*未提供引數，則會使用目前的工作階段的語言。 此語言是以 SET LANGUAGE 陳述式隱含或明確加以設定。 *文化特性*任何.NET Framework; 所支援的文化特性並不限於使用明確支援的語言[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*文化特性*引數無效，PARSE 會引發錯誤。  
  
## <a name="return-types"></a>傳回類型  
 傳回轉譯成所要求之資料類型的運算式結果。  
  
## <a name="remarks"></a>備註  
 以引數形式傳遞給 PARSE 的 Null 值，會以下列兩種方式處理：  
  
1.  如果傳遞了 NULL 常數就會引發錯誤。 Null 值無法以特定文化特定方式剖析為不同的資料類型。  
  
2.  如果在執行階段傳遞了 null 值的參數，將會傳回 null，以避免整個批次遭到取消。  
  
 PARSE 僅適用於從字串轉換到日期/時間及數字類型。 一般類型轉換仍可繼續使用 CAST 或 CONVERT。 請注意，剖析字串值將對效能造成一定程度的負擔。  
  
 PARSE 必須仰賴的.NET Framework Common Language Runtime (CLR)。  
  
 因為必須要有 CLR 才可執行此函數，所以無法從遠端進行。 從遠端處理需要 CLR 的函數，會導致遠端伺服器發生錯誤。  
  
 **Data_type 參數的詳細資訊**  
  
 值*data_type*參數會限制為下表，與樣式中所顯示的類型。 此處所提供的樣式資訊可以協助您決定所要允許的模式類型。 如需有關樣式的詳細資訊，請參閱.NET Framework 文件**System.Globalization.NumberStyles**和**DateTimeStyles**列舉型別。  
  
|類別目錄|類型|.NET Framework 類型|使用的樣式|  
|--------------|----------|-------------------------|-----------------|  
|數值|bigint|Int64|NumberStyles.Number|  
|數值|int|Int32|NumberStyles.Number|  
|數值|smallint|Int16|NumberStyles.Number|  
|數值|tinyint|Byte|NumberStyles.Number|  
|數值|decimal|Decimal|NumberStyles.Number|  
|數值|numeric|Decimal|NumberStyles.Number|  
|數值|float|Double|NumberStyles.Float|  
|數值|real|Single|NumberStyles.Float|  
|數值|smallmoney|Decimal|NumberStyles.Currency|  
|數值|money|Decimal|NumberStyles.Currency|  
|日期及時間|date|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期及時間|time|TimeSpan|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期及時間|datetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期及時間|smalldatetime|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期及時間|datetime2|DateTime|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
|日期及時間|datetimeoffset|DateTimeOffset|DateTimeStyles.AllowWhiteSpaces &#124;DateTimeStyles.AssumeUniversal|  
  
 **文化特性參數的詳細資訊**  
  
 下表顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語言所對應的 .NET Framework 文化特性。  
  
|全名|別名|LCID|專屬文化特性|  
|---------------|-----------|----------|----------------------|  
|us_english|英文|1033|zh-TW|  
|Deutsch|德文|1031|de-DE|  
|Français|法文|1036|fr-FR|  
|日本語|日文|1041|ja-JP|  
|Dansk|丹麥文|1030|da-DK|  
|Español|西班牙文|3082|es-ES|  
|Italiano|義大利文|1040|it-IT|  
|Nederlands|荷蘭文|1043|nl-NL|  
|Norsk|挪威文|2068|nn-NO|  
|Português|葡萄牙文|2070|pt-PT|  
|Suomi|芬蘭文|1035|fi|  
|Svenska|瑞典文|1053|sv-SE|  
|čeština|捷克文|1029|Cs-CZ|  
|magyar|匈牙利文|1038|Hu-HU|  
|polski|波蘭文|1045|Pl-PL|  
|română|羅馬尼亞文|1048|Ro-RO|  
|hrvatski|克羅埃西亞文|1050|hr-HR|  
|slovenčina|斯洛伐克文|1051|Sk-SK|  
|slovenski|斯洛維尼亞文|1060|Sl-SI|  
|ελληνικά\|希臘文|1032|El-GR|  
|български|保加利亞文|1026|bg-BG|  
|русский|俄文|1049|Ru-RU|  
|Türkçe|土耳其文|1055|Tr-TR|  
|British|英式英文|2057|en-GB|  
|eesti|愛沙尼亞文|1061|Et-EE|  
|latviešu|拉脫維亞文|1062|lv-LV|  
|lietuvių|立陶宛文|1063|lt-LT|  
|Português (Brasil)|巴西文|1046|pt-BR|  
|繁體中文|繁體中文|1028|zh-TW|  
|한국어|韓文|1042|Ko-KR|  
|简体中文|簡體中文|2052|zh-CN|  
|阿拉伯文|阿拉伯文|1025|ar-SA|  
|ไทย|泰文|1054|Th-TH|  
  
## <a name="examples"></a>範例  
  
### <a name="a-parse-into-datetime2"></a>A. 剖析為 datetime2  
  
```  
SELECT PARSE('Monday, 13 December 2010' AS datetime2 USING 'en-US') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-13 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-parse-with-currency-symbol"></a>B. 使用貨幣符號進行剖析  
  
```  
SELECT PARSE('€345,98' AS money USING 'de-DE') AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
345.98  
  
(1 row(s) affected)  
```  
  
### <a name="c-parse-with-implicit-setting-of-language"></a>C. 使用語言的隱含設定進行剖析  
  
```  
-- The English language is mapped to en-US specific culture  
SET LANGUAGE 'English';  
SELECT PARSE('12/16/2010' AS datetime2) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------  
2010-12-16 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
  
