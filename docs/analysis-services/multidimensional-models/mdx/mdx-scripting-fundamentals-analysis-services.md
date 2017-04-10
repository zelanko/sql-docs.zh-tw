---
title: "MDX 指令碼基礎觀念 (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "Cube [Analysis Services], 指令碼"
  - "計算 [Analysis Services], 指令碼"
  - "MDX [Analysis Services], 指令碼"
  - "指令碼 [MDX]"
  - "Cube [Analysis Services], 計算"
  - "多維度運算式 [Analysis Services], 指令碼"
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 34
---
# MDX 指令碼基礎觀念 (Analysis Services)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，多維度運算式 (MDX) 指令碼是由一或多個 MDX 運算式或陳述式構成，利用計算擴展 Cube。  
  
 MDX 指令碼可定義 Cube 的計算處理序。 MDX 指令碼也會被視為 Cube 本身的一部分。 因此，變更與 Cube 相關的 MDX 指令碼，會立即變更 Cube 的計算處理序。  
  
 若要建立 MDX 指令碼，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中的 Cube 設計師。 如需詳細資訊，請參閱[定義指派和其他指令碼命令](../../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md) [Introduction to MDX Scripting in Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892) (Microsoft SQL Server 2005 中 MDX 指令碼的簡介)。  
  
 如需 MDX 查詢和計算的效能相關問題，請參閱 [SQL Server Analysis Services Performance Guide](http://go.microsoft.com/fwlink/p/?LinkId=399050) (SQL Server Analysis Services 效能指南) 中的＜MDX optimization (MDX 最佳化)＞一節。  
  
## 本節內容  
  
|主題|說明|  
|-----------|-----------------|  
|[基本 MDX 指令碼 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)|詳細說明基本的 MDX 指令碼，包括每個 Cube 提供的預設 MDX 指令碼，以及在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，MDX 指令碼一般會如何在 Cube 內運作。|  
|[管理範圍及內容 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/managing-scope-and-context-mdx.md)|描述如何使用 [CALCULATE](../Topic/CALCULATE%20Statement%20\(MDX\).md) 陳述式、[SCOPE](../Topic/SCOPE%20Statement%20\(MDX\).md) 陳述式及 [This](../../../mdx/this-mdx.md) 函數，管理 MDX 指令碼內的內容與範圍。|  
|[使用變數與參數 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|描述如何使用 MDX 指令碼中的變數與參數。|  
|[錯誤處理 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/error-handling-mdx.md)|說明 MDX 指令碼內的錯誤處理。|  
|[支援的 MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/supported-mdx-mdx.md)|提供 MDX 指令碼內支援的 MDX 運算子、陳述式及函數的清單。|  
  
## 請參閱＜  
 [MDX 語言參考 &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)  
  
  