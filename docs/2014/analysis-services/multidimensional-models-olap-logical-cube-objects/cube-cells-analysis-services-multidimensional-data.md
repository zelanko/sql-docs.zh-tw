---
title: Cube 資料格 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- storing data [Analysis Services], cells
- hierarchies [Analysis Services], cells
- OLAP objects [Analysis Services], cells
- data members [Analysis Services]
- cubes [Analysis Services], cells
- empty cells [Analysis Services]
- nonleaf members
- cubes [Analysis Services], examples
- storage [Analysis Services], cells
- nonleaf cells
- calculated cells [Analysis Services]
- dimensions [Analysis Services], cells
- cells [Analysis Services]
- leaf members
- leaf cells
ms.assetid: 9945773c-a43b-40d4-91cf-3d2ebc90bca5
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7aa2ea7d9c2c5ee124a4d5643892d788c1a0b612
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330718"
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>Cube 資料格 (Analysis Services - 多維度資料)
  Cube 是由資料格所組成，而依據量值群組和維度來進行組織。 資料格代表 Cube 內每個維度之某個成員於 Cube 內的唯一邏輯交集。 例如，下圖所描述的 Cube 包含一個具有兩個量值的量值群組，並依 Source、Route 和 Time 這三個維度來進行組織。  
  
 ![識別的單一儲存格的 cube 圖表](../../../2014/analysis-services/dev-guide/media/as-cubeintro5.gif "識別的單一儲存格的 Cube 圖表")  
  
 在這個圖表中具有陰影的單一資料格是下列成員的交集：  
  
-   Route 維度的 air 成員。  
  
-   Source 維度的 Africa 成員。  
  
-   Time 維度的 4th quarter 成員。  
  
-   封裝量值。  
  
## <a name="leaf-and-nonleaf-cells"></a>分葉資料格與非分葉資料格  
 Cube 中資料格的值可以使用下列方式之一取得。 在上述範例中，儲存格的值可以直接從擷取事實資料表的 cube，因為用來識別該資料格的所有成員都是*分葉成員*。 依階層而言，分葉成員沒有子成員，而且通常會參考維度資料表中的單一記錄。 此類型的資料格指*分葉資料格*。  
  
 不過，資料格可以也使用識別*非分葉成員*。 非分葉成員是擁有一或多個子成員的成員。 在此狀況下，資料格的值通常是從與非分葉成員相關聯之子成員的彙總衍生。 例如，以下成員與維度的交叉點引用由彙總提供數值的資料格：  
  
-   Route 維度的 air 成員。  
  
-   Source 維度的 Africa 成員。  
  
-   Time 維度的 2nd half 成員。  
  
-   封裝成員。  
  
 Time 維度的 2nd half 成員就是非分葉成員。 因此，與它相關的所有值都必須是彙總值，如下列圖表所示。  
  
 ![第 3 和 4th quarter 資料格的 2nd half 成員](../../../2014/analysis-services/dev-guide/media/as-cubeintro6.gif "2nd half 成員的第 3 和 4th quarter 資料格")  
  
 假設 3rd quarter 和 4th quarter 成員的彙總就是總和，則所指定資料格的值就是 400，而這個值是上圖中所有具有陰影之分葉資料格的總和。 儲存格的值衍生自其他資料格的彙總，因為指定的資料格會被視為*非分葉資料格*。  
  
 針對使用自訂積存的成員和成員群組所衍生的資料格值以及自訂成員，都是以類似的方式處理。 然而，針對導出成員所衍生的資料格值完全是以用來定義導出成員的多維度運算式 (MDX) 運算式為基礎；在某些情況下，可能並未包含任何實際的資料格資料。 如需詳細資訊，請參閱 <<c0> [ 父子式維度中的自訂 Rollup 運算子](../multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md)，[定義的自訂成員公式](../multidimensional-models/attribute-properties-define-custom-member-formulas.md)，並[計算](../multidimensional-models-olap-logical-cube-objects/calculations.md)。  
  
## <a name="empty-cells"></a>空資料格  
 並非 Cube 中的每個資料格都需要包含值；Cube 中可以有不具任何資料的交集。 因為並非在 Cube 中具有量值之維度屬性的每一個交集在事實資料表中都包含對應的記錄，所以這些交集 (稱為空資料格) 會經常出現在 Cube 中。 Cube 的 cube 中的資料格總數中的空白資料格的比例經常被稱為*稀疏性*的 cube。  
  
 例如，下列圖表顯示之 Cube 的結構與本主題中的其他範例類似。 但在本範例中，第三季沒有空運往非洲的貨物，第四季沒有空運往澳洲的貨物。 事實資料表中沒有資料可支援那些維度和量值的交集；因此，那些交集的資料格會是空的。  
  
 ![識別空白資料格的 cube 圖表](../../../2014/analysis-services/dev-guide/media/as-cubeintro7.gif "識別空白資料格的 Cube 圖表")  
  
 在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，空資料格是具有特殊品質的資料格。 因為空資料格會扭曲交叉聯結、計數等的結果，所以許多 MDX 函數會針對計算用途提供忽略空資料格的能力。 如需詳細資訊，請參閱 <<c0> [ 多維度運算式&#40;MDX&#41;參考](/sql/mdx/multidimensional-expressions-mdx-reference)，以及[MDX 的關鍵概念&#40;Analysis Services&#41;](../multidimensional-models/key-concepts-in-mdx-analysis-services.md)。</c0>  
  
## <a name="security"></a>Security  
 資料格資料的存取是在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的角色層級中進行管理，且可使用 MDX 運算式進行細微的控制。 如需詳細資訊，請參閱 <<c0> [ 授與對維度資料的自訂存取&#40;Analysis Services&#41;](../multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)，以及[授與對資料格資料的自訂存取&#40;Analysis Services&#41;](../multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [Cube 儲存區&#40;Analysis Services-多維度資料&#41;](../multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [彙總和彙總設計](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
