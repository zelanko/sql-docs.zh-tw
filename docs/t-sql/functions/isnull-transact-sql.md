---
title: "ISNULL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISNULL
- ISNULL_TSQL
- IFNULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- replacing null values
- null values [SQL Server], ISNULL
- null values [SQL Server], replacement values
- ISNULL function
ms.assetid: 6f3e5802-864b-4e77-9862-657bb5430b68
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8d364548d3303de493343365bd16677ffdfd5641
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="isnull-transact-sql"></a>ISNULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  以指定的取代值來取代 NULL。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ISNULL ( check_expression , replacement_value )  
```  
  
## <a name="arguments"></a>引數  
 *check_expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)NULL 檢查。 *check_expression*可以是任何類型。  
  
 *replacement_value*  
 如果要傳回的運算式*check_expression*是 NULL。 *replacement_value*必須可以隱含地轉換成的型別之型別的*check_expresssion*。  
  
## <a name="return-types"></a>傳回類型  
 會傳回相同的型別*check_expression*。 如果常值 NULL 提供做為*check_expression*，傳回的資料型別*replacement_value*。 如果常值 NULL 提供做為*check_expression* ，而且沒有*replacement_value*提供，會傳回**int**。  
  
## <a name="remarks"></a>備註  
 值*check_expression*如果它不會傳回 NULL; 否則*replacement_value*之後會隱含地轉換成的型別傳回*check_expression*，如果類型不相同。 *replacement_value*如果被截斷*replacement_value*超過*check_expression*。  
  
> [!NOTE]  
>  使用[COALESCE &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)傳回第一個非 null 值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-isnull-with-avg"></a>A. 使用 ISNULL 搭配 AVG  
 下列範例會尋找所有產品的加權平均值。 它會在 `50` 資料表的 `Weight` 資料行中，用值 `Product` 來取代所有 NULL 項目。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### <a name="b-using-isnull"></a>B. 使用 ISNULL  
 下列範例會選取 `AdventureWorks2012` 中所有特殊供應項目的描述、折扣百分比、最小數量和最大數量。 如果所有特殊供應項目的最大數量是 NULL，結果集所顯示的 `MaxQty` 便是 `0.00`。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  Description       |  DiscountPct    |   MinQty    |   最大數量       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Mountain-100 Cl   |  0.35           |   0         |   0                  |
|  運動 Helmet Di   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0.30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  運動 Helmet Di   |  0.15           |   0         |   0                  |
|  LL 道路 Frame S   |  0.35           |   0         |   0                  |
|  休閒車 3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0.20           |   0         |   0                  |
|  半價格 Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### <a name="c-testing-for-null-in-a-where-clause"></a>C. 在 WHERE 子句中測試 NULL  
 請勿使用 ISNULL 來尋找 NULL 值。 請改用 IS NULL。 下列範例會尋找加權資料行中有 `NULL` 的所有產品。 請注意 `IS` 和 `NULL` 之間的空格。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-isnull-with-avg"></a>D. 使用 ISNULL 搭配 AVG  
 下列範例會尋找範例資料表中的所有產品的加權平均值。 它會在 `50` 資料表的 `Weight` 資料行中，用值 `Product` 來取代所有 NULL 項目。  
  
```  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### <a name="e-using-isnull"></a>E. 使用 ISNULL  
 下列範例會使用 ISNULL 來測試 NULL 值資料行中`MinPaymentAmount`並顯示的值`0.00`這些資料列。  
  
```  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 以下為部分結果集。  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  自行車關聯       |     0.0000         |
|  Bike Store                |     0.0000         |
|  循環商店                |     0.0000         |
|  太好了自行車公司     |     0.0000         |
|  典型的自行車購買         |   200.0000         |
|  可接受的銷售與服務  |     0.0000         |
  
### <a name="f-using-is-null-to-test-for-null-in-a-where-clause"></a>F. 使用 IS NULL 來測試為 NULL 的 WHERE 子句中  
 下列範例會尋找所有產品`NULL`中`Weight`資料行。 請注意 `IS` 和 `NULL` 之間的空格。  
  
```  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [為 NULL &#40;TRANSACT-SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [聯合 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  


