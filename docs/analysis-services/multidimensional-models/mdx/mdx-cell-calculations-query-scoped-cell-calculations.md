---
title: 建立查詢範圍資料格計算 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c9cb6f083751b14ad3cd8f2ffaac692ef4e6eb86
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022835"
---
# <a name="mdx-cell-calculations---query-scoped-cell-calculations"></a>MDX 資料格計算查詢範圍資料格計算
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  您可以使用多維度運算式 (MDX) 的 **WITH** 關鍵字，描述查詢內容中的導出資料格。 **WITH** 關鍵字有下列語法：  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 `CellCalc_Identifier` 值是導出資料格的名稱。 `String_Expression` 值包含正交、一維的 MDX 集合運算式。 每個集合運算式都必須解析為下表列出的其中一種類別目錄。  
  
|類別目錄|說明|  
|--------------|-----------------|  
|空集合|解析成空集合的 MDX 命名集運算式。 在此情況下，導出資料格的範圍是整個 Cube。|  
|單一成員集合|解析成單一成員集合的 MDX 命名集運算式。|  
|單一層級成員|解析成單一層級成員的 MDX 命名集運算式。 *Level_Expression*.**Members** MDX 函數是這類集合運算式的範例。 若要包括導出成員，請使用 *Level_Expression*.**AllMembers** MDX 函數。 如需詳細資訊，請參閱 [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md)。|  
|下階集合|解析為指定成員之下階的 MDX 集合運算式。 **Descendants**(*Member_Expression*, *Level_Expresion*, *Desc_Flag*) MDX 函數是這類集合運算式的範例。 如需詳細資訊，請參閱 [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md)。|  
  
 如果 `String_Expression` 引數未描述維度，MDX 會假設已包含所有成員以供建構計算 Subcube。 因此，如果 `String_Expression` 引數是 NULL，導出資料格定義就會套用到整個 Cube。  
  
 `MDX_Expression` 引數包含一個 MDX 運算式，此運算式會將 `String_Expression` 引數中定義的所有資料格評估為資料格值。  
  
## <a name="additional-considerations"></a>其他考量  
 **CONDITION** 屬性指定的計算條件，MDX 只會處理一次。 這個單次處理特性提高了評估多重導出資料格定義時的效能，特別是在 Cube 傳遞之間有重疊的導出資料格時。  
  
 發生單次處理的時機，視導出資料格定義的建立範圍而定：  
  
-   如果做為 Cube 的一部份建立在全域範圍，MDX 會在處理 Cube 時處理計算條件。 如果您以任何方式修改 Cube 中的資料格，而且資料格包含在導出資料格定義的計算 Subcube 中，則在重新處理 Cube 之前，計算條件可能不正確。 例如，進行回寫可能會修改資料格。 重新處理 Cube 時就會重新處理計算條件。  
  
-   如果建立在工作階段範圍，那麼在工作階段期間發出陳述式時，MDX 就會處理計算條件。 與全域建立的導出資料格定義一樣，如果修改資料格的話，導出資料格定義的計算條件可能不正確。  
  
-   如果建立在查詢範圍，MDX 會在查詢執行時處理計算條件。 資料格修改問題在這裏也適用，但是因為 MDX 查詢執行的處理時間很短，所以資料延遲問題會減到最少。  
  
 另一方面，每當對 Cube (涉及導出資料格定義中包含的資料格) 發出 MDX 查詢時，MDX 就會處理計算公式。 不管建立範圍為何，都會發生這個處理。  
  
## <a name="see-also"></a>另請參閱  
 [建立 CELL CALCULATION 陳述式 & #40;MDX & #41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)  
  
  
