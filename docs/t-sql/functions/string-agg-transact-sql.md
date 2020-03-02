---
title: STRING_AGG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords:
- STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d67efc13e326808b570fc33f054f922e74d5923e
ms.sourcegitcommit: cebf41506a28abfa159a5dd871b220630c4c4504
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/20/2020
ms.locfileid: "77478486"
---
# <a name="string_agg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

能串連字串運算式的值，並在這些值之間放置分隔符號值。 系統不會在字串結尾處加入分隔符號。 
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>引數

*expression*  
這是任何類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。 在串連期間，運算式會轉換成 `NVARCHAR` 或 `VARCHAR` 類型。 非字串類型會轉換成 `NVARCHAR` 類型。

*separator*  
這是 `NVARCHAR` 或 `VARCHAR` 類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，用來作為串連字串的分隔符號。 這可以是常值或變數。 

<order_clause>   
選擇性地使用 `WITHIN GROUP` 子句指定串連結果的順序：

```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
<order_by_expression_list>   
 
  非常數[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的清單，可用來排序結果。 每個查詢只允許一個 `order_by_expression`。 預設排序順序為遞增。   
  
## <a name="return-types"></a>傳回型別

傳回類型取決於第一個引數 (運算式)。 如果輸入引數是字串類型 (`NVARCHAR`、`VARCHAR`)，結果類型將會與輸入類型相同。 下表列出自動轉換：  

|輸入運算式類型 |結果 | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR(1...4000) |NVARCHAR(4000) |
|VARCHAR(1...8000) |VARCHAR(8000) |
|int、bigint、smallint、tinyint、numeric、float、real、bit、decimal、smallmoney、money、datetime、datetime2 |NVARCHAR(4000) |

## <a name="remarks"></a>備註

`STRING_AGG` 是一種彙總函式，此函數可擷取資料列中的所有運算式，並將它們串連成單一字串。 運算式值會以隱含方式轉換為字串類型，然後再行串連。 隱含轉換成字串會遵循現有的資料類型轉換規則。 如需有關資料類型轉換的詳細資訊，請參閱 [CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)。 

如果輸入運算式為 `VARCHAR` 類型，則分隔符號不得為 `NVARCHAR` 類型。 

系統會忽略 Null 值，而且不會加入對應的分隔符號。 若要傳回 Null 值的預留位置，請使用 `ISNULL` 函數，如範例 B 中所示。

`STRING_AGG` 可在任何相容性層級使用。

## <a name="examples"></a>範例

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. 產生名稱的清單，並以新行分隔

下列範例會在單一結果資料格中產生一份名稱的清單，並以歸位字元分隔這些名稱。
```sql
USE AdventureWorks2016
GO
SELECT STRING_AGG (CONVERT(nvarchar(max),FirstName), CHAR(13)) AS csv 
FROM Person.Person;  
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

在 `name` 資料格中找到的 `NULL` 值不會在結果中傳回。   

> [!NOTE]  
> 如果使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 查詢編輯器，[以方格顯示結果]  選項將無法實作歸位字元。 請切換至 [以文字顯示結果]  以正確地查看結果集。       
> 根據預設，[以文字顯示結果] 會截斷為 256 個字元。 若要增加此限制，請變更 [每個資料行中顯示的最大字元數]  選項。

### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. 產生以逗號分隔且不含 NULL 值的名稱清單

下列範例會將 Null 值取代為 'N/A'，並在單一結果資料格中傳回以逗號分隔的名稱。  
```sql
USE AdventureWorks2016
GO
SELECT STRING_AGG(CONVERT(nvarchar(max),ISNULL(FirstName,'N/A')), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

> [!NOTE]
> 會顯示修剪過的結果。

|csv | 
|--- |
|Syed,Catherine,Kim,Kim,Kim,Hazem,Sam,Humberto,Gustavo,Pilar,Pilar, ...|  

### <a name="c-generate-comma-separated-values"></a>C. 產生以逗號分隔的值

```sql
USE AdventureWorks2016
GO
SELECT STRING_AGG(CONVERT(nvarchar(max),CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')')), CHAR(13)) AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

> [!NOTE]
> 會顯示修剪過的結果。

|名稱 |
|--- |
|Ken Sánchez (Feb  8 2003 12:00AM) <br />Terri Duffy (Feb 24 2002 12:00AM) <br />Roberto Tamburello (Dec  5 2001 12:00AM) <br />Rob Walters (Dec 29 2001 12:00AM) <br />... |

> [!NOTE]  
> 如果使用 Management Studio 查詢編輯器，[以方格顯示結果]  選項將無法實作歸位字元。 請切換至 [以文字顯示結果]  以正確地查看結果集。

### <a name="d-return-news-articles-with-related-tags"></a>D. 傳回具有相關標籤的新聞文章

文件及其標籤會分成不同的資料表。 開發人員希望針對每篇文章傳回單一資料列，並提供所有相關的標籤。 使用下列查詢：

```sql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags
FROM dbo.Article AS a
LEFT JOIN dbo.ArticleTag AS t
    ON a.ArticleId = t.ArticleId
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|articleId |title |tags |
|--- |--- |--- |
|172 |Polls indicate close election results |politics,polls,city council |
|176 |New highway expected to reduce congestion |NULL |
|177 |Dogs continue to be more popular than cats |polls,animals|

> [!NOTE]
> 若 `STRING_AGG` 函式不是 `SELECT` 清單中的唯一項目，則 `GROUP BY` 子句為必要項目。

### <a name="e-generate-list-of-emails-per-towns"></a>E. 產生每個鄉鎮的電子郵件清單

下列查詢會尋找員工的電子郵件地址，並依城市分組：

```sql
USE AdventureWorks2016
GO

SELECT TOP 10 City, STRING_AGG(CONVERT(nvarchar(max), EmailAddress), ';') AS emails 
FROM Person.BusinessEntityAddress AS BEA  
INNER JOIN Person.Address AS A ON BEA.AddressID = A.AddressID
INNER JOIN Person.EmailAddress AS EA ON BEA.BusinessEntityID = EA.BusinessEntityID 
GROUP BY City;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

> [!NOTE]
> 會顯示修剪過的結果。

|City |電子郵件 |
|--- |--- |
|Ballard|paige28@adventure-works.com;joshua24@adventure-works.com;javier12@adventure-works.com;...|
|Baltimore|gilbert9@adventure-works.com|
|Barstow|kristen4@adventure-works.com|
|Basingstoke Hants|dale10@adventure-works.com;heidi9@adventure-works.com|
|Baytown|kelvin15@adventure-works.com|
|Beaverton|billy6@adventure-works.com;dalton35@adventure-works.com;lawrence1@adventure-works.com;...|
|Bell Gardens|christy8@adventure-works.com
|Bellevue|min0@adventure-works.com;gigi0@adventure-works.com;terry18@adventure-works.com;...|
|Bellflower|philip0@adventure-works.com;emma34@adventure-works.com;jorge8@adventure-works.com;...|
|Bellingham|christopher23@adventure-works.com;frederick7@adventure-works.com;omar0@adventure-works.com;...|

在電子郵件資料行中傳回的電子郵件，可以直接用來傳送電子郵件給在一些特定城市工作的人員群組。 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. 產生每個鄉鎮的排序電子郵件清單   
與上一個範例相類似，下列查詢會尋找員工的電子郵件地址，依城市分組，並按字母順序排序電子郵件：   

```sql
USE AdventureWorks2016
GO

SELECT TOP 10 City, STRING_AGG(CONVERT(nvarchar(max), EmailAddress), ';') WITHIN GROUP (ORDER BY EmailAddress ASC) AS emails 
FROM Person.BusinessEntityAddress AS BEA  
INNER JOIN Person.Address AS A ON BEA.AddressID = A.AddressID
INNER JOIN Person.EmailAddress AS EA ON BEA.BusinessEntityID = EA.BusinessEntityID 
GROUP BY City;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

> [!NOTE]
> 會顯示修剪過的結果。

|City |電子郵件 |
|--- |--- |
|Barstow|kristen4@adventure-works.com
|Basingstoke Hants|dale10@adventure-works.com;heidi9@adventure-works.com
|Braintree|mindy20@adventure-works.com
|Bell Gardens|christy8@adventure-works.com
|Byron|louis37@adventure-works.com
|Bordeaux|ranjit0@adventure-works.com
|Carnation|don0@adventure-works.com;douglas0@adventure-works.com;george0@adventure-works.com;...|
|Boulogne-Billancourt|allen12@adventure-works.com;bethany15@adventure-works.com;carl5@adventure-works.com;...|
|Berkshire|barbara41@adventure-works.com;brenda4@adventure-works.com;carrie14@adventure-works.com;...|
|Berks|adriana6@adventure-works.com;alisha13@adventure-works.com;arthur19@adventure-works.com;...|

## <a name="see-also"></a>另請參閱
 
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [彙總函式 &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

