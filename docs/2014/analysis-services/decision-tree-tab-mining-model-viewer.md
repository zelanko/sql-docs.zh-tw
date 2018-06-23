---
title: 決策樹索引標籤 （採礦模型檢視器） |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.decisiontree.f1
ms.assetid: dc88606f-ba7c-4f8d-af65-bfa17ec16e2b
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8ac997463e15b862dafbb5e561e9ab5dd29601b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035778"
---
# <a name="decision-tree-tab-mining-model-viewer"></a>決策樹索引標籤 (採礦模型檢視器)
  [決策樹] 窗格會顯示決策樹模型中建立之決策規則的視覺表示。 決策規則描述朝向某個特定結果的路徑。  
  
 **如需詳細資訊，請參閱** [Microsoft 決策樹演算法](data-mining/microsoft-decision-trees-algorithm.md)、[使用 Microsoft 樹狀檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 在目前採礦結構中選擇採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視器**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用自訂檢視器，或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 採礦內容檢視器。 還可以使用外掛程式檢視器 (如果有)。  
  
 **放大**  
 放大以取得決策樹中節點和分支的更詳細檢視。 在複雜模型中，決策樹可能有多個分支層級。  
  
 **縮小**  
 縮小以取得樹狀結構的整體檢視。  
  
 **複製圖表檢視**  
 將圖表的可見部分複製到剪貼簿。  
  
 **複製整個圖表**  
 將整個圖表複製到剪貼簿。  
  
 **將圖表縮放至視窗大小**  
 縮小圖表，直到畫面能容納整個樹狀結構為止。  
  
 **長條圖**  
 選取每個節點之長條圖中可顯示的狀態數目。 如果模型中的狀態數目少於所選的值，則不顯示其他長條。  
  
 **樹狀結構**  
 選擇要在檢視器中顯示的樹狀目錄。 如果建立一個包含多個可預測屬性的模型，則演算法會為每個可預測屬性建立單獨的樹狀目錄。  
  
 **背景**  
 選擇可預測屬性的值，用來表示每個節點的背景色彩。 例如，在範例 AdventureWorks 模型中，如果 [背景] 設定為 1 ([Bike Buyer] = Yes)，則當自行車購買者的比例較大時，節點會具有較深的陰影。 此選項提供有關樹狀目錄中分支和節點之意義的其他視覺化提示。  
  
 **預設展開**  
 從清單中選擇值，可設定樹狀圖形中所顯示層級數目的預設值。  
  
 **顯示層級**  
 向右或向左移動滑動軸，可調整樹狀圖形中顯示的層級數目。 若要查看模型中的所有節點，請將滑動軸一直向右移動。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  