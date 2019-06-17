---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = azuresqldb-current||=azure-sqldw-latest||>= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: aab93a133a8dcfeaea96ffa1886ccfcb20936f95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65947472"
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

資料表值函式，會根據指定的分隔符號字元，將字串分割成子字串資料列。

#### <a name="compatibility-level-130"></a>相容性層級 130

STRING_SPLIT 需要為至少 130 的相容性層級。 當層級小於 130 時，SQL Server 無法找到 STRING_SPLIT 函式。

若要變更資料庫的相容性層級，請參閱[檢視或變更資料庫的相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  

```sql
STRING_SPLIT ( string , separator )  
```

## <a name="arguments"></a>引數

 *string*  
 這是任何字元類型 (例如 **nvarchar**、**varchar**、**nchar** 或 **char**) 的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 *separator*  
 這是任何字元類型 (例如 **nvarchar(1)** 、**varchar(1)** 、**nchar(1)** 或 **char(1)** ) 的單一字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，可作為串連子字串的分隔符號。  
  
## <a name="return-types"></a>傳回類型  

傳回資料列為子字串的單資料行資料表。 資料行的名稱是 **value**。 如果任何輸入引數是 **nvarchar** 或 **nchar**，則傳回 **nvarchar**。 否則傳回 **varchar**。 傳回類型的長度與字串引數的長度相同。  
  
## <a name="remarks"></a>Remarks  

**STRING_SPLIT** 輸入有已分隔之子字串的字串，並輸入一個字元作為分隔符號 (delimiter) 或分隔符號 (separator)。 STRING_SPLIT 輸出單一資料行資料表，其資料列包含子字串。 輸出資料行的名稱為 **value**。

輸出資料列可能為任何順序。 子字串的順序「不」  保證與輸入字串的相同。 您可以在 SELECT 陳述式上使用 ORDER BY 子句的 (`ORDER BY value`)，以覆寫最終的排序次序。

當輸入字串包含兩個或更多個連續出現的分隔符號字元時，會出現長度為零的空白子字串。 空白子字串視為純文字子字串來處理。 您可以使用 WHERE 子句將包含空白字串的任何資料列篩選掉 (`WHERE value <> ''`)。 如果輸入字串是 NULL，則 STRING_SPLIT 資料表值函數會傳回空白資料表。  

例如，下列 SELECT 陳述式使用空白字元作為分隔符號：

```sql
SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');
```

在練習執行中，上述 SELECT 傳回下列結果資料表：  
  
|value|  
| :-- |  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
| &nbsp; |

## <a name="examples"></a>範例  
  
### <a name="a-split-comma-separated-value-string"></a>A. 分割逗號分隔值字串

剖析值的逗號分隔清單，並傳回所有非空白的權杖：  

```sql
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
|1|Full-Finger Gloves|clothing,road,touring,bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
下列查詢會轉換每個標記清單，並將它們與原始資料列結合：  

```sql  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|[屬性]|value|  
|---------------|----------|-----------|  
|1|Full-Finger Gloves|clothing|  
|1|Full-Finger Gloves|road|  
|1|Full-Finger Gloves|touring|  
|1|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  

  >[!NOTE]
  > 輸出順序可能會有所不同，因為該順序「不」  保證與輸入字串中的子字串順序相符。
  
### <a name="c-aggregation-by-values"></a>C. 依據值彙總

使用者必須建立顯示每個標籤之產品數的報告，依據產品數排序，並僅篩選超過兩個產品的標籤。  

```sql  
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

```sql
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```

尋找有兩個指定標籤 (clothing 和 road) 的產品：  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road'));  
```

### <a name="e-find-rows-by-list-of-values"></a>E. 依據值清單來尋找資料列

開發人員必須建立依據識別碼清單尋找發行項的查詢。 他們可以使用下列查詢：  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')
    ON value = ProductId;  
```  

上述 STRING_SPLIT 使用方式是常見反面模式的替代作法。 這種反面模式可涉及在應用程式層中或在 Transact-SQL 中建立動態 SQL 字串。 反面模式也可以使用 LIKE 運算子來達成。 請參閱下列範例 SELECT 陳述式：

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```

## <a name="see-also"></a>另請參閱

[LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)<br />
[LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)<br />
[RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)<br />
[RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)<br />
[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)<br />
[TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)<br />
[字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
