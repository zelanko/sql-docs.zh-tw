---
title: 運算式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77ef7250c7af3918509e38c9aa1f5350f3ac5610
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690837"
---
# <a name="expressions-mdx"></a>運算式 (MDX)


  運算式是識別碼、 數值與運算子，可以評估以取得結果的組合。 在存取或變更資料時，資料可以用在許多不同的地方。 例如，您可以使用運算式做為查詢所要擷取之資料的一部份、或是做為搜尋條件來尋找符合一組條件的資料。  
  
## <a name="simple-and-complex-expressions"></a>簡單及複雜運算式  
 MDX 中的運算式可能很簡單或很複雜：  
  
 簡單運算式可以是下列運算式之一：  
  
 常數  
 常數在 MDX 中是代表單一特定值的符號。 字串、數值及日期值可以轉譯成常數。 和數值常數不同，字串及日期常數必須以單引號 (') 字元分隔。  
  
 純量函數  
 在 MDX 中，純量函數會傳回評估內容內的單一值。 因為不只會在單一資料元素上，也會反覆在一群資料元素 (例如，資料格或成員) 上評估大部份的 MDX 運算式、陳述式及指令碼，所以此特性對了解 MDX 如何解析純量函數很重要。 但是，在評估純量函數時，此函數一般會檢閱單一資料元素。  
  
 物件識別碼  
 因為多維度資料的本質，所以 MDX 是物件導向的。 物件識別碼在 MDX 中視為簡單運算式。 如需有關識別碼的詳細資訊，請參閱[識別碼&#40;MDX&#41;](../mdx/identifiers-mdx.md)。  
  
 複雜運算式可以從上述項目利用運算子聯結的組合來建立。  
  
## <a name="expression-results"></a>運算式結果  
 對於由單一常數、變數、純量函數或資料行名稱組成的簡單運算式，其運算式的資料類型、整數位數、小數位數與值就是參照元素的資料型別、整數位數、小數位數與值。 因為 MDX 只會直接支援 OLE VARIANT 資料類型，所以使用簡單運算式時不應該發生強制型轉。  
  
 對於複雜運算式，使用兩個以上具有不同資料類型的簡單運算式時，才能發生強制型轉。  
  
## <a name="expression-examples"></a>運算式範例  
 下列查詢會顯示定義為簡單運算式的導出量值範例：  
  
 `WITH`  
  
 `MEMBER MEASURES.CONSTANTVALUE AS 1`  
  
 `MEMBER MEASURES.SCALARFUNCTION AS [Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.OBJECTIDENTIFIER AS [Measures].[Internet Sales Amount]`  
  
 `SELECT {MEASURES.CONSTANTVALUE,MEASURES.SCALARFUNCTION,MEASURES.OBJECTIDENTIFIER } ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 運算式也可以進行計算，例如 `[Measures].[Discount Amount] * 1.5`。 以下範例示範計算的用法，在 MDX SELECT 陳述式中定義成員：  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[使用 Cube 及 Subcube 運算式](../mdx/using-cube-and-subcube-expressions.md)|描述 Cube 及 Subcube 運算式。|  
|[使用維度運算式](../mdx/using-dimension-expressions.md)|定義維度運算式。|  
|[使用成員運算式](../mdx/using-member-expressions.md)|定義成員運算式。|  
|[使用 Tuple 運算式](../mdx/using-tuple-expressions.md)|定義 Tuple 運算式。|  
|[使用集合運算式](../mdx/using-set-expressions.md)|定義集合運算式。|  
|[使用純量運算式](../mdx/using-scalar-expressions.md)|定義純量運算式。|  
|[使用空白值](../mdx/working-with-empty-values.md)|描述什麼是空白值，以及如何處理這類的值。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 語言參考 &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
