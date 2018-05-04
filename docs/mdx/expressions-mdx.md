---
title: 運算式 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- identifiers [MDX]
- expressions [MDX]
- expressions [MDX], about expressions
- MDX [Analysis Services], expressions
- Multidimensional Expressions [Analysis Services], expressions
ms.assetid: e20c34bc-30fa-4ac5-b896-9d4c9925ef59
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a158bbcdd77e4a7e1e026db793b46e306d8c6fbe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="expressions-mdx"></a>運算式 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  運算式是識別碼、 數值與運算子的組合， [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]可以評估而取得結果。 在存取或變更資料時，資料可以用在許多不同的地方。 例如，您可以使用運算式做為查詢所要擷取之資料的一部份、或是做為搜尋條件來尋找符合一組條件的資料。  
  
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
  
|主題|Description|  
|-----------|-----------------|  
|[使用 Cube 及 Subcube 運算式](../mdx/using-cube-and-subcube-expressions.md)|描述 Cube 及 Subcube 運算式。|  
|[使用維度運算式](../mdx/using-dimension-expressions.md)|定義維度運算式。|  
|[使用成員運算式](../mdx/using-member-expressions.md)|定義成員運算式。|  
|[使用 Tuple 運算式](../mdx/using-tuple-expressions.md)|定義 Tuple 運算式。|  
|[使用集合運算式](../mdx/using-set-expressions.md)|定義集合運算式。|  
|[使用純量運算式](../mdx/using-scalar-expressions.md)|定義純量運算式。|  
|[使用空白值](../mdx/working-with-empty-values.md)|描述什麼是空白值，以及如何處理這類的值。|  
  
## <a name="see-also"></a>另請參閱  
 [MDX 語言參考 & #40;MDX & #41;](../mdx/mdx-language-reference-mdx.md)   
 [MDX 查詢基礎觀念 & #40;Analysis Services & #41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
