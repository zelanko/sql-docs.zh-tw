---
title: 建立查詢範圍命名集（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- query-scoped named sets [MDX]
- WITH keyword
ms.assetid: 78bc1e9a-1bc4-4a5a-ab0b-cf430c8fbfe1
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6eccb4e20fca03079a04a0219b07f6411b80a433
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546310"
---
# <a name="creating-query-scoped-named-sets-mdx"></a>建立查詢範圍命名集 (MDX)
  如果單一多維度運算式 (MDX) 查詢只需要有命名集，您可以使用 WITH 關鍵字來定義命名集。 查詢完成執行之後，使用 WITH 關鍵字建立的命名集就不再存在。  
  
 如同本主題所討論，WITH 關鍵字的語法很有彈性，甚至可以使用函數來定義命名集。  
  
> [!NOTE]  
>  如需命名集的詳細資訊，請參閱[在 MDX 中建立命名集 &#40;MDX&#41;](mdx-named-sets-building-named-sets.md)。  
  
## <a name="with-keyword-syntax"></a>WITH 關鍵字語法  
 使用以下語法將 WITH 關鍵字加入 MDX SELECT 陳述式：  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
   ( SET Set_Identifier AS 'Set_Expression')  
  
```  
  
 在 WITH 關鍵字的語法中， `Set_Identifier` 參數包含命名集的別名。 `Set_Expression` 參數包含了命名集別名所參考的集合運算式。  
  
## <a name="with-keyword-example"></a>WITH 關鍵字範例  
 下列 MDX 查詢會檢查 `FoodMart 2000` (Microsoft SQL Server 2000 Analysis Services 的範例資料庫) 中，各種 Chardonnay 和 Chablis 葡萄酒的單位銷售量。 此查詢就結果集而言雖然相當簡單，但當您必須維護這樣的查詢時卻是冗長而不便的。  
  
```  
SELECT  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]} ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
 若要使先前的 MDX 查詢易於維護，您可以使用 WITH 關鍵字來為查詢建立命名集。 以下程式碼顯示如何使用 WITH 關鍵字建立命名集 `[ChardonnayChablis]`，以及命名集如何使 SELECT 陳述式變得更短也更容易維護。  
  
```  
WITH SET [ChardonnayChablis] AS  
   {[Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chardonnay],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Good].[Good Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Pearl].[Pearl Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Portsmouth].[Portsmouth Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Top Measure].[Top Measure Chablis Wine],  
   [Product].[All Products].[Drink].[Alcoholic Beverages].[Beer and Wine].[Wine].[Walrus].[Walrus Chablis Wine]}  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
```  
  
### <a name="using-functions-together-with-the-with-keyword"></a>函數搭配 WITH 關鍵字一起使用  
 雖然您可以明確定義命名集的每個成員，但這種方式會產生一個冗長的陳述式。 若要讓建立和維護命名集更容易，您可以使用 MDX 函數來定義成員。  
  
 例如，下列 MDX 查詢範例使用 [Filter](/sql/mdx/filter-mdx)、 [CurrentMember](/sql/mdx/current-mdx)、 [Name](/sql/mdx/members-string-mdx) MDX 函數以及 InStr VBA 函數，來建立 `[ChardonnayChablis]` 命名集。 這個 `[ChardonnayChablis]` 命名集版本和先前在本主題中顯示的明確定義版本相同。  
  
```  
WITH SET [ChardonnayChablis] AS  
   'Filter([Product].Members, (InStr(1, [Product].CurrentMember.Name, "chardonnay") <> 0) OR (InStr(1, [Product].CurrentMember.Name, "chablis") <> 0))'  
  
SELECT  
   [ChardonnayChablis] ON COLUMNS,  
   {Measures.[Unit Sales]} ON ROWS  
FROM Sales  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [SELECT 語句 &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [建立工作階段範圍命名集 &#40;MDX&#41;](mdx-named-sets-creating-session-scoped-named-sets.md)  
  
  
