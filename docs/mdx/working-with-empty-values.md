---
description: 使用空白值
title: 使用空白值 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f497ba1ccf84ac642144340af4d5597d773dcadb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421892"
---
# <a name="working-with-empty-values"></a>使用空白值


  空白值代表特定成員、Tuple 或資料格為空白。 空白資料格值代表在基礎事實資料表中找不到指定資料格的資料，或指定資料格的 Tuple 代表不適用於 Cube 的成員組合。  
  
> [!NOTE]  
>  雖然空白值跟零值不同，但一般會將空白值視為零。  
  
 下列查詢說明空值和零值的行為：  
  
```  
WITH  
//A calculated Product Category that always returns 0  
MEMBER [Product].[Category].[All Products].ReturnZero AS 0  
//Will return true for any null value  
MEMBER MEASURES.ISEMPTYDemo AS ISEMPTY([Measures].[Internet Tax Amount])  
//Will true for any null or zero value  
//To be clear: the expression 0=null always returns true in MDX  
MEMBER MEASURES.IsZero AS [Measures].[Internet Tax Amount]=0  
SELECT  
{[Measures].[Internet Tax Amount],MEASURES.ISEMPTYDemo,MEASURES.IsZero}  
ON COLUMNS,  
[Product].[Category].[Category].ALLMEMBERS  
ON ROWS  
FROM [Adventure Works]  
WHERE([Date].[Calendar].[Calendar Year].&[2001])  
```  
  
 以下資訊適用於零值：  
  
-   只有當函數中指定的元組所識別的資料格是空的時， [IsEmpty](../mdx/isempty-mdx.md) 函式才會傳回 **TRUE** 。 否則，函數會傳回 **FALSE**。  
  
    > [!NOTE]  
    >  **IsEmpty**函數無法判斷成員運算式是否會傳回 null 值。 若要判斷是否從運算式傳回 null 成員，請使用 [ [是](../mdx/is-mdx.md)] 運算子。  
  
-   當空白資料格值是任一個數值運算子 (+、-、*、/) 的運算元時，如果其他運算元不是空值，就會將空白資料格值視為零。 如果兩個運算元都是空的，則數值運算子會傳回空白資料格值。  
  
-   當空白資料格值是字串串連運算子 (+) 的運算元時，如果其他運算元不是空值，就會將空白資料格值視為空白字串。 如果兩個運算元都是空的，則字串串連運算子會傳回空白資料格值。  
  
-   當空的資料格值是任一個比較運算子 (=. <>、>=、 \<=, > <) ，則會將空白資料格值視為零或空字串，取決於另一個運算元的資料類型是否分別為數值或字串。 如果兩個運算元都是空白，則會將兩個運算元視為零。  
  
-   當定序數值時，空白資料格值會定序在和零相同的位置。 對於空白資料格值和零兩者，空白資料格定序在零的前面。  
  
-   當定序字串值時，空白資料格值會定序在和空白字串相同的位置。 對於空白資料格值和空白字串兩者，空定序在空白字串的前面。  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>處理 MDX 陳述式及 Cube 中的空白值  
 在多維度運算式 (MDX) 陳述式中，您可以尋找空白值，然後以有效 (也就是說，非空白) 資料在資料格上執行特定計算。 在執行計算時，消除空值非常重要，因為某些特定計算 (例如取平均值) 如果將空白資料格值包含在內，結果可能會不正確。  
  
 如果空值儲存在基礎事實資料表資料中，預設會在處理 cube 時將這些值轉換成零。 您可以在量值上使用 **Null 處理** 選項，以控制是否要將 null 事實轉換成0、轉換為空值，或甚至在處理期間擲回錯誤。 如果您不希望查詢結果中有空的資料格值出現，您應該建立查詢、導出成員或 MDX 指令碼陳述式來刪除空白值，或是以某個其他值取代空白值。  
  
 若要從查詢中移除空白資料列或資料行，您可以在軸設定定義之前使用 NON EMPTY 陳述式。 例如，下列查詢只會傳回 Product Category Bikes，因為這是在 Calendar Year 2001 唯一賣出的 Category：  
  
 `SELECT`  
  
 `{[Measures].[Internet Tax Amount]}`  
  
 `ON COLUMNS,`  
  
 `//Comment out the following line to display all the empty rows for other Categories`  
  
 `NON EMPTY`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
 一般來說，若要從集合中移除空白 tuple，您可以使用 NonEmpty 函數。 下列查詢顯示兩個導出量值，其中一個會計算 Product Category 的數目，另一個會顯示具有 [Internet Tax Amount] 量值和 Calendar Year 2001 值的 Product Category 數目：  
  
 `WITH`  
  
 `MEMBER MEASURES.CategoryCount AS`  
  
 `COUNT([Product].[Category].[Category].MEMBERS)`  
  
 `MEMBER MEASURES.NonEmptyCategoryCountFor2001 AS`  
  
 `COUNT(`  
  
 `NONEMPTY(`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `,([Date].[Calendar].[Calendar Year].&[2001], [Measures].[Internet Tax Amount])`  
  
 `))`  
  
 `SELECT`  
  
 `{MEASURES.CategoryCount,MEASURES.NonEmptyCategoryCountFor2001 }`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 如需詳細資訊，請參閱非空白的 [&#40;MDX&#41;](../mdx/nonempty-mdx.md)。  
  
## <a name="empty-values-and-comparison-operators"></a>空白值及比較運算子  
 當資料中有空白值時，邏輯與比較運算子可能會傳回第三種結果 EMPTY，而非只有 TRUE 或 FALSE。 這種三重數值邏輯的需要是造成應用程式錯誤的來源。 下表大致說明導入空白值比較的結果。  
  
 這個表格會顯示將 AND 運算子套用到兩個布林 (Boolean) 運算元的結果。  
  
|AND|true|EMPTY|false|  
|---------|----------|-----------|-----------|  
|**TRUE**|true|false|false|  
|**空**|false|EMPTY|false|  
|**FALSE**|false|false|false|  
  
 這個表格會顯示將 OR 運算子套用到兩個布林運算元的結果。  
  
|或者|true|false|  
|--------|----------|-----------|  
|**TRUE**|TRUE|TRUE|  
|**空**|TRUE|TRUE|  
|**FALSE**|true|false|  
  
 這個表格會顯示 NOT 運算子如何取消或反轉布林運算子的結果。  
  
|套用 NOT 運算子的布林運算式|評估為|  
|-------------------------------------------------------------|------------------|  
|true|false|  
|EMPTY|EMPTY|  
|false|true|  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 函數參考 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Mdx 運算子參考 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX &#40;運算式&#41;](../mdx/expressions-mdx.md)  
  
  
