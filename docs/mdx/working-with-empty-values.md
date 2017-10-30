---
title: "使用空白值 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- expressions [MDX], empty values
- empty values [MDX]
ms.assetid: 6338fb85-f513-4c3e-a774-4fd7c6986a91
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: aef26d6b575ca340111054824fe024e81c6f7115
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="working-with-empty-values"></a>使用空白值
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
-   [IsEmpty](../mdx/isempty-mdx.md)函式會傳回**TRUE**如果且只有在函式中指定的 tuple 所識別的資料格是空的。 否則，函數會傳回**FALSE**。  
  
    > [!NOTE]  
    >  **IsEmpty** 函式無法判斷成員運算式是否會傳回 null 值。 若要判斷是否要從運算式傳回 null 成員，請使用[IS](../mdx/is-mdx.md)運算子。  
  
-   當空白資料格值是任一個數值運算子 (+、-、*、/) 的運算元時，如果其他運算元不是空值，就會將空白資料格值視為零。 如果兩個運算元都是空的，則數值運算子會傳回空白資料格值。  
  
-   當空白資料格值是字串串連運算子 (+) 的運算元時，如果其他運算元不是空值，就會將空白資料格值視為空白字串。 如果兩個運算元都是空的，則字串串連運算子會傳回空白資料格值。  
  
-   當空的資料格值是任一個比較運算子 (=. <>，> =、 \<=、 >、 <)、 空白資料格值視為零或空字串，根據資料的另一個運算元的類型是否可為數值或字串，分別。 如果兩個運算元都是空白，則會將兩個運算元視為零。  
  
-   當定序數值時，空白資料格值會定序在和零相同的位置。 對於空白資料格值和零兩者，空白資料格定序在零的前面。  
  
-   當定序字串值時，空白資料格值會定序在和空白字串相同的位置。 對於空白資料格值和空白字串兩者，空定序在空白字串的前面。  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>處理 MDX 陳述式及 Cube 中的空白值  
 在多維度運算式 (MDX) 陳述式中，您可以尋找空白值，然後以有效 (也就是說，非空白) 資料在資料格上執行特定計算。 在執行計算時，消除空值非常重要，因為某些特定計算 (例如取平均值) 如果將空白資料格值包含在內，結果可能會不正確。  
  
 如果空值儲存在基礎事實資料表資料中，預設會在處理 cube 時將這些值轉換成零。 您可以使用**Null 處理**選項來控制量值是否也將 null 事實轉換成 0，轉換成空白的值或甚至會擲回錯誤處理期間。 如果您不希望查詢結果中有空的資料格值出現，您應該建立查詢、導出成員或 MDX 指令碼陳述式來刪除空白值，或是以某個其他值取代空白值。  
  
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
  
 如需詳細資訊，請參閱[NonEmpty &#40;MDX &#41;](../mdx/nonempty-mdx.md).  
  
## <a name="empty-values-and-comparison-operators"></a>空白值及比較運算子  
 當資料中有空白值時，邏輯與比較運算子可能會傳回第三種結果 EMPTY，而非只有 TRUE 或 FALSE。 這種三重數值邏輯的需要是造成應用程式錯誤的來源。 下表大致說明導入空白值比較的結果。  
  
 這個表格會顯示將 AND 運算子套用到兩個布林 (Boolean) 運算元的結果。  
  
|與|TRUE|EMPTY|FALSE|  
|---------|----------|-----------|-----------|  
|**為 TRUE**|TRUE|FALSE|FALSE|  
|**空白**|FALSE|EMPTY|FALSE|  
|**FALSE**|FALSE|FALSE|FALSE|  
  
 這個表格會顯示將 OR 運算子套用到兩個布林運算元的結果。  
  
|OR|TRUE|FALSE|  
|--------|----------|-----------|  
|**為 TRUE**|TRUE|TRUE|  
|**空白**|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|  
  
 這個表格會顯示 NOT 運算子如何取消或反轉布林運算子的結果。  
  
|套用 NOT 運算子的布林運算式|評估為|  
|-------------------------------------------------------------|------------------|  
|TRUE|FALSE|  
|EMPTY|EMPTY|  
|FALSE|TRUE|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 函數參考 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 運算子參考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [運算式 &#40;MDX &#41;](../mdx/expressions-mdx.md)  
  
  

