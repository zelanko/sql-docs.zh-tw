---
title: FORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 87750e264f87b8244cb74b9d68276c85d92e5761
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59670927"
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

傳回以 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中指定的格式與選用文化特性格式化的值。 將 FORMAT 函數用於將日期/時間與數值視為字串的地區設定感知格式化作業。 針對一般資料類型轉換，請使用 CAST 或 CONVERT。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```sql
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>引數

 *value*  
 要格式化之受支援資料類型的運算式。 如需有效類型的清單，請參閱下面＜備註＞一節中的表格。  
  
 *format*  
 **nvarchar** 格式模式。  
  
 *format* 引數必須包含有效的 .NET Framework 格式字串，其可以是標準格式字串 (例如 "C" 或 "D")，也可以是日期與數值的自訂字元模式 (如 "MMMM DD, yyyy (dddd)")。 不支援複合格式。 如需這些格式模式的完整說明，請參閱 .NET Framework 文件中有關一般字串格式、自訂日期與時間格式，以及自訂數字格式的資訊。 您不妨從「[格式類型](https://go.microsoft.com/fwlink/?LinkId=211776)」主題開始著手。  
  
 *culture*  
 指定文化特性的選用 **nvarchar** 引數。  
  
 如未提供 *culture* 引數，將會使用目前工作階段的語言。 此語言是以 SET LANGUAGE 陳述式隱含或明確加以設定。 *culture* 的引數可以是 .NET Framework 所支援的任何文化特性，而不限於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 明確支援的語言。 如果 *culture* 引數無效，FORMAT 會引發錯誤。  
  
## <a name="return-types"></a>傳回類型

 **nvarchar** 或 null  
  
 傳回值的長度取決於 *format*。  
  
## <a name="remarks"></a>Remarks

 FORMAT 會針對不是 *valid* 的 *culture* 以外的錯誤傳回 NULL。 例如，如果 *format* 中指定的值無效，則會傳回 NULL。  

 FORMAT 函數不具決定性。
  
 FORMAT 必須仰賴既存的 .NET Framework Common Language Runtime (CLR)。  
  
 因為必須要有 CLR 才可以執行此函數，所以無法從遠端進行。 從遠端處理需要 CLR 的函數可能會導致遠端伺服器發生錯誤。  
  
 FORMAT 會依賴 CLR 格式規則，這些規則規定必須逸出冒號和句號。 因此，當格式字串 (第二個參數) 包含冒號或句號時，如果輸入值 (第一個參數) 屬於 **time** 資料類型，則必須以反斜線逸出冒號或句號。 請參閱 [D. 具有 time 資料類型的 FORMAT](#ExampleD)。  
  
 下表列出 *value* 引數可接受的資料類型，以及其 .NET Framework 對應的對等類型。  
  
|類別目錄|類型|.NET 類型|  
|--------------|----------|---------------|  
|數值|BIGINT|Int64|  
|數值|ssNoversion|Int32|  
|數值|SMALLINT|Int16|  
|數值|TINYINT|Byte|  
|數值|Decimal|SqlDecimal|  
|數值|NUMERIC|SqlDecimal|  
|數值|FLOAT|Double|  
|數值|REAL|Single|  
|數值|SMALLMONEY|Decimal|  
|數值|money|Decimal|  
|日期及時間|日期|DateTime|  
|日期及時間|time|TimeSpan|  
|日期及時間|DATETIME|DateTime|  
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

 下列範例會藉由指定自訂格式顯示格式數值。 此範例假設目前的日期為 2012 年 9 月 27 日。 如需有關這些自訂格式和其他自訂格式的詳細資訊，請參閱[自訂數值格式字串](https://msdn.microsoft.com/library/0c899ak8.aspx)。  
  
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

 下列範例會從 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的 **Sales.CurrencyRate** 資料表傳回 5 個資料列。 **EndOfDateRate** 資料行會以 **money** 類型，儲存在資料表中。 在此範例中，資料行會以未格式化的狀態傳回，然後藉由指定 .NET Number 格式、General 格式和 Currency 格式類型進行格式化。 如需有關這些數值格式和其他數值格式的詳細資訊，請參閱[標準數值格式字串](https://msdn.microsoft.com/library/dwhawy9k.aspx)。  
  
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
  
### <a name="ExampleD"></a> D. 具有 time 資料類型的 FORMAT

 FORMAT 會在這些情況下傳回 NULL，因為未逸出 `.` 和 `:`。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 Format 會傳回格式化的字串，因為會逸出 `.` 和 `:`。  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>另請參閱

 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
