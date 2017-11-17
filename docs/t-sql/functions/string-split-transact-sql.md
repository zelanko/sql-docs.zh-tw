---
title: "STRING_SPLIT (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 049bdf1021d57e28ed94e11c89aa997ee0eba5e5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  將使用指定的分隔符號的字元運算式。  
  
> [!NOTE]  
>  **STRING_SPLIT**函式是僅適用於相容性等級 130。 如果您的資料庫相容性層級低於 130，SQL Server 將無法找出並執行**STRING_SPLIT**函式。 您可以使用下列命令變更資料庫的相容性層級：  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  請注意，相容性層級 120 可能甚至會在新的 Azure SQL Database 中的預設值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>引數  
 *string*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的任何字元類型 (也就是**nvarchar**， **varchar**， **nchar**或**char**)。  
  
 *分隔符號*  
 是單一字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的任何字元類型 (例如**nvarchar(1)**， **varchar(1)**， **nchar(1)**或**char （1)**)，可當做分隔符號的串連字串。  
  
## <a name="return-types"></a>傳回類型  
 傳回單一資料行包含資料表的片段。 資料行的名稱是**值**。 傳回**nvarchar**如果任何輸入引數都是**nvarchar**或**nchar**。 否則會傳回**varchar**。 字串引數的長度相同的傳回類型的長度。  
  
## <a name="remarks"></a>備註  
 **STRING_SPLIT**採用應該被除數的字串，並將用來分割字串的分隔符號。 它會傳回子字串的單一資料行資料表。 例如，下列陳述式`SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');`使用做為分隔符號，空格字元會傳回下列結果資料表：  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|位置|  
|amet。|  
  
 如果輸入的字串為**NULL**、 **STRING_SPLIT**資料表值函式會傳回空白資料表。  
  
 **STRING_SPLIT**至少需要 130 的相容性模式。  
  
## <a name="examples"></a>範例  
  
### <a name="a-split-comma-separated-value-string"></a>A. 以分割的逗號分隔的數值字串  
 剖析值的逗號分隔清單，並傳回所有非空白的語彙基元：  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 如果沒有任何分隔符號之間 STRING_SPLIT 會傳回空字串。 條件 RTRIM(value) <> ' 將會移除空的語彙基元。  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. 以分割的逗號分隔的資料行中的值字串  
 Product 資料表有逗號個別清單的標記顯示在下列範例中的資料行：  
  
|productId|名稱|Tags|  
|---------------|----------|----------|  
|1|完整手指手套|clothing touring，自行車的道路|  
|2|LL 耳機|自行車|  
|3|HL Mountain Frame|自行車、 mountain|  
  
 下列查詢來轉換每個清單的標記，並結合與原始的資料列：  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|productId|名稱|value|  
|---------------|----------|-----------|  
|1|完整手指手套|clothing|  
|1|完整手指手套|路段圖|  
|1|完整手指手套|touring|  
|1|完整手指手套|自行車|  
|2|LL 耳機|自行車|  
|3|HL Mountain Frame|自行車|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>C. 值的彙總  
 使用者必須建立的報表會顯示每個每個標記，依數字的產品，以及篩選的標記具有 2 個以上產品的產品數目。  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. 標記值來搜尋  
 開發人員必須建立查詢以尋找關鍵字的文件。 他們可以使用下列查詢：  
  
 若要尋找單一標籤 (clothing) 的產品：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 尋找產品與兩個指定的標記 （clothing 和 road）：  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. 值清單來尋找資料列  
 開發人員必須建立查詢，以尋找發行項識別碼的清單。 他們可以使用下列查詢：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 這是常見的反向模式，例如應用程式層中建立的動態 SQL 字串取代或[!INCLUDE[tsql](../../includes/tsql-md.md)]，或使用 LIKE 運算子：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>另請參閱  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [子字串 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)  
  
  

