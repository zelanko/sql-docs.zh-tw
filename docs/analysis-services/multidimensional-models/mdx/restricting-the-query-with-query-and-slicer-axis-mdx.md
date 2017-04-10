---
title: "利用查詢與 Slicer 軸限制查詢 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "多維度運算式 [Analysis Services], 軸"
  - "查詢 [MDX], 軸"
  - "axes [MDX]"
  - "MDX [Analysis Services], 軸"
ms.assetid: a64b8172-cd73-42f9-8847-52e967b9697a
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 利用查詢與 Slicer 軸限制查詢 (MDX)
  在以公式表示多維度運算式 (MDX) SELECT 陳述式時，應用程式一般會檢查 Cube，並將階層集合分割成兩個子集：  
  
-   **查詢座標軸**—為多個成員擷取的資料的階層集合。 如需查詢座標軸的詳細資訊，請參閱[指定查詢座標軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-query-axis-mdx.md)。  
  
-   **Slicer 軸**—為單一成員擷取的資料的階層集合。 如需 Slicer 軸的詳細資訊，請參閱[指定 Slicer 軸的內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/specifying-the-contents-of-a-slicer-axis-mdx.md)。  
  
 因為查詢座標軸與 Slicer 軸可以從即將查詢之 Cube 的多個階層建構，這些用語是用來區別即將查詢的 Cube 所採用的階層跟 MDX 查詢傳回的 Cube 中建立的階層。  
  
 若要查看使用查詢及 Slicer 軸的簡單範例，請參閱[在簡單的範例中使用查詢及 Slicer 軸 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-query-and-slicer-axes-in-a-simple-example-mdx.md)。  
  
## 請參閱＜  
 [使用成員、Tuple 和集合 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  