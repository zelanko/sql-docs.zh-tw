---
title: "建置 MDX (MDX) 中的資料格計算 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculated cells [MDX]
- queries [MDX], cell calculations
- cells [MDX]
- MDX [Analysis Services], calculations
- calculation subcubes [MDX]
- calculated values [MDX]
- Multidimensional Expressions [Analysis Services], cell calculations
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cef256029853aabd5017f610081ed45ac632a935
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-cell-calculations---build-cell-calculations"></a>MDX 資料格計算建置資料格計算
  多維度運算式 (MDX) 為您提供許多產生導出值的工具，如導出成員、自訂積存與自訂成員。 但是，就此而言光使用這些功能，很難影響一組特定的資料格或單一個資料格。  
  
 若要特別為資料格產生導出值，就必須在 MDX 中使用導出資料格功能。 導出資料格功能可讓您定義特定的資料格 Slice (稱為 *「計算 Subcube」*)，並對計算 Subcube 內的每個資料格套用公式，但要視每個資料格適用的選擇性條件而定。  
  
 導出資料格也能提供複雜的功能，例如 KPI 中使用的目標搜尋公式或推測性分析公式。 此功能層級來自 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的行程順序功能，使用行程順序中的特定傳遞所套用的計算公式，允許以導出資料格建立遞迴傳遞。 如需行程順序的詳細資訊，請參閱[了解行程順序和求解順序 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)。  
  
 就建立的範圍而言，導出資料格類似於其中的命名集與導出成員，可以做為 Cube 的一部份供全域使用，也可以在工作階段或單一查詢的存留期間暫時建立。  
  
-   **查詢範圍** ：若要建立一個導出資料格，把它定義為 MDX 查詢的一部份，而且範圍限制在查詢內，請使用 WITH 關鍵字。 然後您就可以在 MDX SELECT 陳述式內使用導出資料格。 使用這種方式，可以變更利用 **WITH** 關鍵字建立的導出資料格，而不會影響到 SELECT 陳述式。  
  
     如需如何使用 WITH 關鍵字建立導出成員的詳細資訊，請參閱 [建立查詢範圍資料格計算 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)。  
  
-   **工作階段範圍** ：若要建立一個範圍超出查詢內容的導出成員，也就是說它的範圍是 MDX 工作階段的存留期間，您可以使用 CREATE CELL CALCULATION 或 ALTER CUBE 陳述式。  
  
     如需如何使用 CREATE CELL CALCULATION 或 ALTER CUBE 陳述式建立工作階段中的導出資料格的詳細資訊，請參閱 [建立工作階段範圍導出資料格](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells.md)  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER CUBE 陳述式 &#40;MDX&#41;](../../../mdx/mdx-data-definition-alter-cube.md)   
 [建立 CELL CALCULATION 陳述式 &#40;MDX &#41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)   
 [建立查詢範圍資料格計算 &#40;MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations.md)   
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
