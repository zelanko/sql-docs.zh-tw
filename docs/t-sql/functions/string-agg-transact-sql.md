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
ms.openlocfilehash: f7dd020c0ec7f68dbd589b6e07026adfab86c890
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75720789"
---
# <a name="string_agg-transact-sql"></a>STRING_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

能串連字串運算式的值，並在這些值之間放置分隔符號值。 系統不會在字串結尾處加入分隔符號。 

在 SQL Server 2017 中導入。
 
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
這是 [ 或 ](../../t-sql/language-elements/expressions-transact-sql.md) 類型的`NVARCHAR`運算式`VARCHAR`，用來作為串連字串的分隔符號。 這可以是常值或變數。 

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
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

在 `NULL` 資料格中找到的 `name` 值不會在結果中傳回。   

> [!NOTE]  
>  如果使用 Management Studio 查詢編輯器，[以方格顯示結果]  選項將無法實作歸位字元。 請切換至 [以文字顯示結果]  以正確地查看結果集。   

### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. 產生以逗號分隔且不含 NULL 值的名稱清單

下列範例會將 Null 值取代為 'N/A'，並在單一結果資料格中傳回以逗號分隔的名稱。  
```sql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Csv | 
|--- |
|John,N/A,Mike,Peter,N/A,N/A,Alice,Bob |  

### <a name="c-generate-comma-separated-values"></a>C. 產生以逗號分隔的值

```sql
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

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
> 若 `GROUP BY` 函式不是 `STRING_AGG` 清單中的唯一項目，則 `SELECT` 子句為必要項目。

### <a name="e-generate-list-of-emails-per-towns"></a>E. 產生每個鄉鎮的電子郵件清單

下列查詢會尋找員工的電子郵件地址，並依鄉鎮分組：

```sql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|鄉鎮 |電子郵件 |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

在電子郵件資料行中傳回的電子郵件，可以直接用來傳送電子郵件給於部分特定鄉鎮工作的人員群組。 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. 產生每個鄉鎮的排序電子郵件清單   
與上一個範例類似，下列查詢會尋找員工的電子郵件地址，依鄉鎮分組，並以字母順序排序電子郵件：   
```sql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|鄉鎮 |電子郵件 |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |

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

