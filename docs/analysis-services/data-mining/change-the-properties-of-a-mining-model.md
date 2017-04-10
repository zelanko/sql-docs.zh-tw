---
title: "變更採礦模型的屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "採礦模型 [Analysis Services], 屬性"
  - "屬性 [資料採礦]"
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 38
---
# 變更採礦模型的屬性
  有些採礦模型屬性可套用至整個模型，有些模型屬性只套用至個別資料行。 例如，**Drillthrough** 屬性可套用至整個模型，它指定案例資料是否應該可用於查詢，**Description** 屬性也是這類屬性。 套用至資料行的屬性包含 **Usage** 和 **ModelingFlags**，它們控制資料行中的資料在模型內的使用方式。  
  
 下列模型屬性具有可用於建立運算式或設定複雜模型屬性的進階編輯器。 下列屬性提供：  
  
-   **Filter**：開啟 [[資料集篩選器] 或 [模型篩選器] 對話方塊](../Topic/Data%20Set%20Filter%20or%20Model%20Filter%20Dialog%20Box.md)。  
  
-   **AlgorithmParameters** 屬性︰開啟 [[演算法參數] 對話方塊 &#40;採礦模型檢視&#41;](../Topic/Algorithm%20Parameters%20Dialog%20Box%20\(Mining%20Models%20View\).md)。  
  
 如需如何在採礦模型中設定屬性的資訊，請參閱[採礦模型資料行](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### 若要變更採礦模型的屬性  
  
1.  在資料採礦設計師的 [採礦模型] 索引標籤中，以滑鼠右鍵按一下包含採礦模型名稱的資料行標題，或方格中包含採礦演算法名稱的資料列，然後選取 [屬性]。  
  
2.  在畫面右側的 [屬性] 視窗中，反白顯示對應到您要變更之屬性的值，然後輸入新值。  
  
     您在設計師中選取其他元素時，新值就會生效。  
  
### 變更採礦模型資料行的屬性  
  
1.  在資料採礦設計師的 [採礦模型] 索引標籤中，以滑鼠右鍵按一下採礦結構資料行和採礦模型交集方格中的資料格，然後選取 [屬性]。  
  
2.  在畫面右側的 [屬性] 視窗中，反白顯示對應到您要變更之屬性的值，然後輸入新值。  
  
    > [!NOTE]  
    >  如果資料行使用方式是設定為 [忽略]，則資料行的 [屬性] 視窗為空白。  
  
     您在設計師中選取其他元素時，新值就會生效。  
  
## 請參閱＜  
 [採礦模型工作和使用說明](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  