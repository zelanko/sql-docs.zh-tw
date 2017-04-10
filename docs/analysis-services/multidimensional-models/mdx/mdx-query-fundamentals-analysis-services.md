---
title: "MDX 查詢基礎觀念 (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
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
  - "陳述式 [MDX]"
  - "多維度運算式 [Analysis Services], 陳述式"
  - "多維度運算式 [Analysis Services], 查詢"
  - "MDX [Analysis Services], 陳述式"
  - "MDX 查詢 [Analysis Services]"
  - "MDX [Analysis Services], 查詢"
  - "查詢 [MDX]"
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 30
---
# MDX 查詢基礎觀念 (Analysis Services)
  您可以使用多維度運算式 (MDX) 查詢多維度物件 (例如 Cube)，然後傳回包含 Cube 資料的多維度資料格集。 這個主題以及子主題將提供對 MDX 查詢的概觀。  
  
 以下主題描述 MDX 查詢與其產生的資料格集，並提供有關基本 MDX 語法更詳細的資訊。  
  
> [!NOTE]  
>  如需 MDX 查詢和計算相關效能問題的詳細資訊，請參閱 [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621) (SQL Server 2005 Analysis Services 效能指南) 的 “Writing Efficient MDX” (＜撰寫有效率的 MDX＞) 一節。  
  
## 本節內容  
  
|主題|說明|  
|-----------|-----------------|  
|[基本 MDX 查詢 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-query-mdx.md)|提供 MDX SELECT 陳述式的基本語法資訊。|  
|[利用查詢與 Slicer 軸限制查詢 &#40;MDX&#41;](../Topic/Restricting%20the%20Query%20with%20Query%20and%20Slicer%20Axes%20\(MDX\).md)|描述什麼是查詢及 Slicer 軸，以及如何指定它們。|  
|[建立查詢中的 Cube 內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|描述 MDX SELECT 陳述式中 FROM 子句的目的。|  
|[在 MDX 中建立命名集 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md)|描述 MDX 中命名集的用途，以及在 MDX 查詢中建立和使用它們所需的技巧。|  
|[在 MDX 中建立導出成員 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md)|提供有關 MDX 中導出成員的資訊，包括在 MDX 運算式中建立和使用它們所需的技巧。|  
|[在 MDX 中建立資料格計算 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-cell-calculations-in-mdx-mdx.md)|詳述建立與使用導出資料格的程序。|  
|[建立和使用屬性值 &#40;MDX&#41;](../Topic/Creating%20and%20Using%20Property%20Values%20\(MDX\).md)|詳述建立和使用維度、層級、成員及資料格屬性的程序。|  
|[操作資料 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/manipulating-data-mdx.md)|描述使用鑽研及積存功能操作資料背後的基本知識，還會描述 MDX 中的行程順序及解決順序。|  
|[修改資料 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/modifying-data-mdx.md)|描述如何使用回寫，暫時或永久地變更多維度資料。|  
|[使用變數與參數 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|描述如何在 MDX 查詢中使用變數和參數。|  
  
## 請參閱＜  
 [多維度運算式 &#40;MDX&#41 參考](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  