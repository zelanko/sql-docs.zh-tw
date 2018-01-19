---
title: "格式 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/15/2017
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
- FORMAT_TSQL
- FORMAT
dev_langs: TSQL
helpviewer_keywords: FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 46c7becb151b1942b411aefe337717172f207bb9
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回以 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中指定的格式與選用文化特性格式化的值。 將 FORMAT 函數用於將日期/時間與數值視為字串的地區設定感知格式化作業。 針對一般資料類型轉換，請使用 CAST 或 CONVERT。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>引數  
 *value*  
 要格式化之受支援資料類型的運算式。 如需有效類型的清單，請參閱下面＜備註＞一節中的表格。  
  
 *<格式>*  
 **nvarchar**格式模式。  
  
 *格式*引數必須包含有效的.NET Framework 格式字串，以標準格式字串 （例如，"C"或"D"），或作為自訂字元模式的日期與數值 (例如，"MMMM DD，yyyy (dddd)"). 不支援複合格式。 如需這些格式模式的完整說明，請參閱在一般字串格式、 自訂日期和時間格式，以及自訂數字格式的.NET Framework 文件。 很好的起點是主題"[格式類型](http://go.microsoft.com/fwlink/?LinkId=211776)。 」  
  
 *culture*  
 選擇性**nvarchar**引數指定文化特性。  
  
 如果*文化特性*未提供引數，會使用目前的工作階段的語言。 此語言是以 SET LANGUAGE 陳述式隱含或明確加以設定。 *文化特性*做為引數;.NET Framework 所支援的任何文化特性並不限於使用明確支援的語言[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*文化特性*引數無效，FORMAT 會引發錯誤。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar**或 null  
  
 傳回值的長度由決定*格式*。  
  
## <a name="remarks"></a>備註  
 格式會傳回 NULL 的錯誤以外*文化特性*不*有效*。 如果在指定的值，例如，傳回 NULL*格式*不正確。  
 
 格式函式不具決定性。   
  
 格式必須仰賴的.NET Framework Common Language Runtime (CLR)。  
  
 此函式無法遠端處理，因為它相依於 CLR 存在。 遠端處理需要 CLR 函式無法在遠端伺服器上造成錯誤。  
  
 格式會依賴 CLR 格式化規則、 聽寫冒號和期間必須逸出。 因此，當的格式字串 （第二個參數） 包含冒號或句點、 冒號或週期必須逸出反斜線時輸入的值 （第一個參數） 是**時間**資料型別。 請參閱[D.格式與時間資料型別](#ExampleD)。  
  
 下表列出的可接受的資料類型*值*以及其.NET Framework 對應對等型別引數。  
  
|類別目錄|型別|.NET 類型|  
|--------------|----------|---------------|  
|數值|bigint|Int64|  
|數值|int|Int32|  
|數值|smallint|Int16|  
|數值|tinyint|Byte|  
|數值|decimal|SqlDecimal|  
|數值|numeric|SqlDecimal|  
|數值|float|Double|  
|數值|real|Single|  
|數值|smallmoney|Decimal|  
|數值|money|Decimal|  
|日期及時間|date|DateTime|  
|日期及時間|time|TimeSpan|  
|日期及時間|datetime|DateTime|  
|日期及時間|smalldatetime|DateTime|  
|日期及時間|datetime2|DateTime|  
|日期及時間|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-format-example"></a>A. 簡單的 FORMAT 範例  
 下列範例會傳回針對不同文化特性格式化的簡單日期。  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';   
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>B. 包含自訂格式字串的 FORMAT  
 下列範例會藉由指定自訂格式顯示格式數值。 此範例假設目前的日期為 2012 年 9 月 27 日。 如需有關這些和其他自訂格式的詳細資訊，請參閱[自訂數值格式字串](http://msdn.microsoft.com/library/0c899ak8.aspx)。  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>C. 數值類型的 FORMAT  
 下列範例會傳回 5 個資料列從**Sales.CurrencyRate**資料表中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]資料庫。 資料行**EndOfDateRate**儲存為類型**money**資料表中。 在此範例中，資料行會以未格式化的狀態傳回，然後藉由指定 .NET Number 格式、General 格式和 Currency 格式類型進行格式化。 如需有關這些和其他數字格式的詳細資訊，請參閱[標準數值格式字串](http://msdn.microsoft.com/library/dwhawy9k.aspx)。  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 此範例會指定德文文化特性 (de-de)。  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
###  <a name="ExampleD"></a> D. 時間資料類型的 FORMAT  
 格式會傳回在這些情況下 NULL 因為`.`和`:`未逸出。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 格式傳回格式化的字串，因為`.`和`:`會逸出。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>另請參閱  
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
