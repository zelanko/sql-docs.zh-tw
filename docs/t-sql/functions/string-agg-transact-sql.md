---
title: "STRING_AGG (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- STRING_AGG
- STRING_AGG_TSQL
helpviewer_keywords: STRING_AGG function
ms.assetid: 8860ef3f-142f-4cca-aa64-87a123e91206
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5eab0444f036b05f23982b6f21455bfc5ab408a8
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="stringagg-transact-sql"></a>STRING_AGG (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

串連字串運算式的值，並將它們之間的分隔符號值。 不會在字串結尾處加入分隔符號。
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STRING_AGG ( expression, separator ) [ <order_clause> ]

<order_clause> ::=   
    WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )   
```

## <a name="arguments"></a>引數 

*分隔符號*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的`NVARCHAR`或`VARCHAR`用做為分隔符號的類型的串連字串。 它可以是常值或變數。 

*expression*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)任何型別。 運算式會轉換成`NVARCHAR`或`VARCHAR`串連在型別。 非字串類型轉換成`NVARCHAR`型別。


< order_clause >   
選擇性地指定順序串連結果使用`WITHIN GROUP`子句：
```
WITHIN GROUP ( ORDER BY <order_by_expression_list> [ ASC | DESC ] )
```   
< order_by_expression_list >   
 
  非常數的清單[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，可用來排序結果。 只有一個`order_by_expression`允許每個查詢。 預設排序順序為遞增。   
  

## <a name="return-types"></a>傳回類型 

傳回型別就會根據第一個引數 （運算式）。 如果輸入引數是字串類型 (`NVARCHAR`， `VARCHAR`)，結果型別會與輸入的類型相同。 下表列出自動轉換：  

|輸入的運算式型別 |結果 | 
|-------|-------|
|NVARCHAR(MAX) |NVARCHAR(MAX) |
|VARCHAR(MAX) |VARCHAR(MAX) |
|NVARCHAR (1...4000) |NVARCHAR （4000) |
|VARCHAR (1...8000) |VARCHAR(8000) |
|int、 bigint、 smallint、 tinyint、 numeric、 float、 real、 位元、 decimal、 smallmoney、 money、 datetime、 datetime2， |NVARCHAR （4000) |


## <a name="remarks"></a>備註  
 
`STRING_AGG`彙總會從資料列的所有運算式，並將它們串連成單一字串。 運算式的值會隱含地轉換成字串類型，並再串連。 隱含轉換成字串會遵循現有的資料類型轉換規則。 如需資料類型轉換的詳細資訊，請參閱[CAST 和 CONVERT (TRANSACT-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)。 

如果輸入的運算式是型別`VARCHAR`，分隔符號不可為型別`NVARCHAR`。 

會忽略 null 值，並不會加入對應的分隔符號。 若要傳回的 null 值的預留位置，請使用`ISNULL`函式 b 範例中所示

`STRING_AGG`可在任何相容性層級。


## <a name="examples"></a>範例 

### <a name="a-generate-list-of-names-separated-in-new-lines"></a>A. 產生新行分隔之名稱的清單 
下列範例會產生一份在單一結果的資料格中，以換行字元分隔的名稱。
```sql
SELECT STRING_AGG (FirstName, CHAR(13)) AS csv 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|csv | 
|--- |
|Syed <br />Catherine <br />Kim <br />Kim <br />Kim <br />Hazem <br />... | 

`NULL`在找到值`name`資料格不會傳回結果中。   
> [!NOTE]  
>  使用 Management Studio 查詢編輯器中，如果**以方格顯示結果**選項不能實作傳回的歸位字元。 切換至**以文字顯示結果**查看結果設定正確無誤。   


### <a name="b-generate-list-of-names-separated-with-comma-without-null-values"></a>B. 產生名稱以不含 NULL 值的逗號分隔的清單   
下列範例取代 'N/A' 的 null 值，並傳回單一結果資料格中的逗號分隔的名稱。  
```sql
SELECT STRING_AGG ( ISNULL(FirstName,'N/A'), ',') AS csv 
FROM Person.Person; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
 

|Csv | 
|--- |
|John、 n/A、 Mike、 Peter、 n/A、 n/A，Alice、 Bob |  


### <a name="c-generate-comma-separated-values"></a>C. 產生以逗號分隔值 

```sql   
SELECT 
STRING_AGG(CONCAT(FirstName, ' ', LastName, ' (', ModifiedDate, ')'), CHAR(13)) 
  AS names 
FROM Person.Person; 
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|名稱 | 
|--- |
|Ken sánchez (2 月 8日 2003 12:00 AM) <br />與 Terri Duffy (年 2 月 24日 2002 12:00 AM) <br />蘇 Tamburello (12 月 5日 2001 12:00 AM) <br />Rob 郭 (12 / 29 2001 12:00 AM) <br />... |

> [!NOTE]  
>  使用 Management Studio 查詢編輯器中，如果**以方格顯示結果**選項不能實作傳回的歸位字元。 切換至**以文字顯示結果**查看結果設定正確無誤。   
 

### <a name="d-return-news-articles-with-related-tags"></a>D. 傳回新聞文章，具有相關的標記 

文件，以及其標籤分成不同的資料表。 開發人員想要傳回的所有相關聯標籤的每一個發行項每一個資料列。 使用下列查詢： 
```sql
SELECT a.articleId, title, STRING_AGG (tag, ',') as tags 
FROM dbo.Article AS a       
LEFT JOIN dbo.ArticleTag AS t 
    ON a.ArticleId = t.ArticleId 
GROUP BY a.articleId, title;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|發行項識別碼 |title |標記 |
|--- |--- |--- |
|172 |輪詢指出關閉選取的結果 |政治、 投票、 縣 （市) council | 
|176 |若要減少壅塞預期新高速公路 |NULL |
|177 |繼續 cats 較常見 dogs |輪詢動物| 

### <a name="e-generate-list-of-emails-per-towns"></a>E. 產生的每個擁有電子郵件的清單

下列查詢會尋找員工的電子郵件地址，並依城鎮分組： 
```sql
SELECT town, STRING_AGG (email, ';') AS emails 
FROM dbo.Employee 
GROUP BY town; 
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|城鎮 |電子郵件 |
|--- |--- |
|Seattle |syed0@adventure-works.com;catherine0@adventure-works.com;kim2@adventure-works.com |
|LA |sam1@adventure-works.com;hazem0@adventure-works.com |

在資料行可以直接用來傳送電子郵件給一群人使用某些特定城鎮電子郵件中，傳回電子郵件。 

### <a name="f-generate-a-sorted-list-of-emails-per-towns"></a>F. 產生已排序的清單，每個擁有電子郵件   
   
類似於上一個範例，下列查詢會尋找員工的電子郵件地址、 城鎮，將它們分組和字母順序排列的電子郵件：   
```sql
SELECT town, 
    STRING_AGG (email, ';') WITHIN GROUP (ORDER BY email ASC) AS emails 
FROM dbo.Employee 
GROUP BY town; 
```
   
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|城鎮 |電子郵件 |
|--- |--- |
|Seattle |catherine0@adventure-works.com;kim2@adventure-works.com;syed0@adventure-works.com |
|LA |hazem0@adventure-works.com;sam1@adventure-works.com |


## <a name="see-also"></a>請參閱  

[字串函數 (TRANSACT-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  

