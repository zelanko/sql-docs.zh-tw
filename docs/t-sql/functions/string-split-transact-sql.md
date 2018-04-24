---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5204f8df5f2267421c27528ef85126e118fe56b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  使用指定的分隔符號來分割字元運算式。  
  
> [!NOTE]  
>  **STRING_SPLIT** 函數僅適用於相容性層級 130 以下。 如果您的資料庫相容性層級低於 130，SQL Server 將找不到且無法執行 **STRING_SPLIT** 函數。 您可以使用下列命令變更資料庫的相容性層級：  
> ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
>   
>  請注意，即使是新的 Azure SQL Database，其預設的相容性層級也可能會是 120。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>引數  
 *string*  
 這是任何字元類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md) (亦即 **nvarchar****varchar****nchar** 或 **char**)。  
  
 *separator*  
 這是用來當作串連字串之分隔符號的任何字元類型的單一字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md) (亦即 **nvarchar(1)****varchar(1)****nchar(1)** 或 **char(1)**)。  
  
## <a name="return-types"></a>傳回類型  
 傳回有片段的單一資料行資料表。 資料行的名稱是 **value**。 如果任何輸入引數是 **nvarchar** 或 **nchar**，則傳回 **nvarchar**。 否則傳回 **varchar**。 傳回類型的長度與字串引數的長度相同。  
  
## <a name="remarks"></a>Remarks  
 **STRING_SPLIT** 會使用應該分割的字串和將用來分割字串的分割符號。 它會傳回有子字串的單一資料行資料表。 例如，使用空白字元當做分隔符號的下列陳述式 `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');`，會傳回下列結果資料表：  
  
|value|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
  
 如果輸入的字串是 **NULL**則 **STRING_SPLIT** 資料表值函數會傳回空白資料表。  
  
 **STRING_SPLIT** 至少需要相容性模式 130。  
  
## <a name="examples"></a>範例  
  
### <a name="a-split-comma-separated-value-string"></a>A. 分割逗號分隔值字串  
 剖析值的逗號分隔清單，並傳回所有非空白的權杖：  
  
```  
  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
  
```  
  
 如果任何分隔符號之間沒有任何內容，則 STRING_SPLIT 會傳回空字串。 條件 RTRIM(value) <> '' 將會移除空白權杖。  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. 分割資料行中的逗號分隔值字串  
 Product 資料表有一個資料行含有標籤的逗號分隔清單，如下列範例所示：  
  
|ProductId|[屬性]|Tags|  
|---------------|----------|----------|  
|@shouldalert|Full-Finger Gloves|clothing,road,touring,bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
 下列查詢會轉換每個標記清單，並將它們與原始資料列結合：  
  
```  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|[屬性]|value|  
|---------------|----------|-----------|  
|@shouldalert|Full-Finger Gloves|clothing|  
|@shouldalert|Full-Finger Gloves|road|  
|@shouldalert|Full-Finger Gloves|touring|  
|@shouldalert|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>C. 依據值彙總  
 使用者必須建立顯示每個標籤之產品數的報告，依據產品數排序，並僅篩選超過 2 個產品的標籤。  
  
```  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. 依據標籤值來搜尋  
 開發人員必須建立依據關鍵字尋找發行項的查詢。 他們可以使用下列查詢：  
  
 若要尋找有單一標籤 (clothing) 的產品：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
 尋找有兩個指定標籤 (clothing 和 road) 的產品：  
  
```  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. 依據值清單來尋找資料列  
 開發人員必須建立依據識別碼清單尋找發行項的查詢。 他們可以使用下列查詢：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
 這是常見反向模式的取代，例如在應用程式層或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中建立動態 SQL 字串，或透過使用 LIKE 運算子：  
  
```  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>另請參閱  
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
  
  
