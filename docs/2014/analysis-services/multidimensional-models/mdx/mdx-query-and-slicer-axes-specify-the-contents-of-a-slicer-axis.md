---
title: 指定交叉分析篩選器軸的內容（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- slicer axis
- filtering data [MDX]
ms.assetid: c56b0a70-cdec-427f-990e-425290344e7d
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8620c54970ea14a2ac01c85262a372d2b3db0d68
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546260"
---
# <a name="specifying-the-contents-of-a-slicer-axis-mdx"></a>指定 Slicer 軸的內容 (MDX)
  Slicer 軸會篩選多維度運算式 (MDX) SELECT 陳述式傳回的資料，限制傳回的資料，以便只傳回與指定成員交集的資料。 它可以視為查詢中隱藏的額外軸。 Slicer 軸定義在 MDX SELECT 陳述式的 WHERE 子句中。  
  
## <a name="slicer-axis-syntax"></a>Slicer 軸語法  
 若要明確指定 Slicer 軸，您可以在 MDX 中使用 `<SELECT slicer axis clause>` ，如以下語法所述：  
  
```  
<SELECT slicer axis clause> ::=  WHERE Set_Expression  
```  
  
 在顯示的 Slicer 軸語法中， `Set_Expression` 可以取得 Tuple 運算式或集合運算式，而 Tuple 運算式會視為一個集合，用於評估子句。 如果已指定集合運算式，MDX 將嘗試評估此集合，彙總集合中每一個 Tuple 的結果資料格。 換句話說，MDX 將會在此集合嘗試使用 [Aggregate](/sql/mdx/aggregate-mdx) 函數，利用與其相關的彙總函式來彙總每個量值。 此外，如果無法將集合運算式表示為屬性階層成員的交叉聯集，MDX 會將 Slicer 落在集合運算式之外的資料格，評估為 Null。  
  
> [!IMPORTANT]  
>  MDX SELECT 陳述式的 WHERE 子句不像 SQL 中的 WHERE 子句，前者絕不會直接篩選查詢的 Rows 軸上傳回的內容。 若要篩選查詢的 Rows 或 Columns 軸上顯示的內容，您可以使用各種不同的 MDX 函數，例如 FILTER、NONEMPTY 和 TOPCOUNT。  
  
### <a name="implicit-slicer-axis"></a>隱含 Slicer 軸  
 如果 Cube 內階層的成員未明確地包含在查詢座標軸中，階層的預設成員就會隱含地包含在 Slicer 軸中。 如需預設成員的詳細資訊，請參閱 [定義預設成員](../attribute-properties-define-a-default-member.md)。  
  
## <a name="examples"></a>範例  
 下列查詢不包含 WHERE 子句，並且會傳回所有 Calendar Year 之 Internet Sales Amount 的量值。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
```  
  
 加入 WHERE 子句，如下所示：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States])  
  
```  
  
 不會改變查詢中 Rows 或 Columns 上傳回的內容；它會改變針對每一個資料格傳回的值。 這個範例會分割查詢，以便傳回所有 Calendar Year 的 Internet Sales Amount 值，不過只包括住在 United States 的 Customer。不同階層的成員可以加入 WHERE 子句中。 下列查詢會針對住在美國 (United States) 並且購買過自行車類別 (Bikes Category) 產品 (Product) 的客戶 Customer)，顯示所有日曆年度 (Calendar Year) 的網際網路銷售量 (Internet Sales Amount) 值。  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE([Customer].[Customer Geography].[Country].&[United States], [Product].[Category].&[1])  
```  
  
 如果您要使用相同階層的多個成員，則需要在 WHERE 子句中包含一個集合。 例如，下列查詢會針對購買過自行車類別 (Category Bikes) 產品 (Product)，並且住在美國 (United States) 或英國 (United Kingdom) 的客戶 Customer)，顯示所有日曆年度 (Calendar Year) 的網際網路銷售量 (Internet Sales Amount) 值：  
  
```  
SELECT {[Measures].[Internet Sales Amount]} ON COLUMNS,  
[Date].[Calendar Year].MEMBERS ON ROWS  
FROM [Adventure Works]  
WHERE(  
{[Customer].[Customer Geography].[Country].&[United States]  
, [Customer].[Customer Geography].[Country].&[United Kingdom]}  
, [Product].[Category].&[1])  
  
```  
  
 如上面所述，在 WHERE 子句中使用集合將隱含地彙總集合中所有成員的值。 在這種情況下，查詢會在每一個資料格中顯示美國和英國的彙總值。  
  
  
