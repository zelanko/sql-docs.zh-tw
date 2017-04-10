---
title: "修改資料 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "修改資料 [MDX]"
  - "多維度運算式 [Analysis Services], 資料修改"
  - "MDX [Analysis Services], 資料修改"
  - "資料修改 [MDX]"
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 修改資料 (MDX)
  除了使用多維度運算式 (MDX) 擷取及處理維度與 Cube 的資料之外，您還可以使用 MDX來更新或「回寫」維度與 Cube 資料。 這些更新可能是暫時性 (如同推測性或 "what if" 分析 ) 或永久性 (例如，必須根據資料分析來變更時)。  
  
 資料的更新可發生在維度或 Cube 層級：  
  
 **維度回寫**  
 您可以使用 [ALTER CUBE 陳述式 (MDX)](../Topic/ALTER%20CUBE%20Statement%20\(MDX\).md) 陳述式來變更可寫入維度的資料，並且使用 [REFRESH CUBE 陳述式 (MDX)](../Topic/REFRESH%20CUBE%20Statement%20\(MDX\).md) 來反映屬性值的刪除、建立及更新。 您也可以使用 ALTER CUBE 陳述式來執行複雜的作業，例如刪除階層中的整個子樹，以及將已刪除成員的子系升級。  
  
 **Cube 回寫**  
 您可以使用 [UPDATE CUBE](../Topic/UPDATE%20CUBE%20Statement%20\(MDX\).md) 陳述式，對可寫入 Cube 進行更新。 您可以使用 UPDATE CUBE 陳述式，來更新具有指定值的 Tuple。 您可以使用 [REFRESH CUBE 陳述式 (MDX)](../Topic/REFRESH%20CUBE%20Statement%20\(MDX\).md)，以伺服器上的更新資料來重新整理用戶端工作階段中的資料。  
  
 如需詳細資訊，請參閱[使用 Cube 回寫 &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-cube-writebacks-mdx.md)。  
  
## 請參閱＜  
 [MDX 查詢基礎觀念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  