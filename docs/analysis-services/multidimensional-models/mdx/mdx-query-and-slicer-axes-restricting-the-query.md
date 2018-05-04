---
title: The query with Query and Slicer 軸 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c19bdf8b4850add274875fbe9af305d56a0aef4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-query-and-slicer-axes---restricting-the-query"></a>MDX 查詢及 Slicer 軸-限制查詢
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  在以公式表示多維度運算式 (MDX) SELECT 陳述式時，應用程式一般會檢查 Cube，並將階層集合分割成兩個子集：  
  
-   **查詢座標軸**—為多個成員擷取的資料的階層集合。 如需查詢座標軸的詳細資訊，請參閱[指定查詢座標軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)。  
  
-   **Slicer 軸**—為單一成員擷取的資料的階層集合。 如需 Slicer 軸的詳細資訊，請參閱[指定 Slicer 軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)。  
  
 因為查詢座標軸與 Slicer 軸可以從即將查詢之 Cube 的多個階層建構，這些用語是用來區別即將查詢的 Cube 所採用的階層跟 MDX 查詢傳回的 Cube 中建立的階層。  
  
 若要查看使用查詢及 Slicer 軸的簡單範例，請參閱[在簡單的範例中使用查詢及 Slicer 軸 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-using-axes-in-a-simple-example.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用成員、 Tuple 及集合 & #40;MDX & #41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [MDX 查詢基礎觀念 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
