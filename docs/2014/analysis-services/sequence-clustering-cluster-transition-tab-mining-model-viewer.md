---
title: 時序群集群集轉換索引標籤 （採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.transition.f1
ms.assetid: 40aef457-d69f-4905-a2d3-924c37bd3d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bada5acfd14b824be79fca692debf1a3479f056d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216638"
---
# <a name="sequence-clustering-cluster-transition-tab-mining-model-viewer"></a>時序叢集的叢集轉換索引標籤 (採礦模型檢視器)
  可以使用 [Microsoft 時序叢集檢視器] 中的 [狀態轉換] 索引標籤，更仔細地查看選定叢集中屬性/值組 (或狀態) 之間的轉換。  
  
 使用此時序叢集模型檢視可檢視模式。 在圖表中，連結代表轉換的機率，而節點代表時序狀態。  
  
 **如需詳細資訊，請參閱** [Microsoft 時序群集演算法](data-mining/microsoft-sequence-clustering-algorithm.md)、[使用 Microsoft 時序叢集檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 選擇包含在目前採礦結構中，您要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視器**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用自訂檢視器，或 **[Microsoft 一般內容樹狀檢視器]**。 還可以使用外掛程式檢視器 (如果有)。  
  
 **放大**  
 將圖表放大，更仔細地查看狀態。  
  
 **縮小**  
 將圖表縮小，以取得叢集中整體的狀態檢視。  
  
 **複製圖表檢視**  
 將圖表的可見部分複製到剪貼簿。  
  
 **複製整個圖表**  
 將整個圖表複製到剪貼簿。  
  
 **Cluster**  
 選擇要在檢視器中顯示的群集。 預設會選取 [母體擴展 (全部)]，這表示整個模型中的狀態和轉換都包含在圖形中。 在選擇某個特定叢集時，僅顯示該叢集中的狀態和轉換。  
  
 **提示：** 可以使用 **[叢集圖表]** 索引標籤，重新命名叢集。只需要選取叢集，以滑鼠右鍵按一下，再選取 [重新命名] 即可。 用更具描述性的標籤重新命名叢集，可使得在 **[狀態轉換]** 索引標籤中比較叢集變得更容易。  
  
 **顯示邊緣標籤**  
 選取此選項可在圖形的每個邊緣上顯示數字來表示轉換機率。  
  
 **連結**  
 使用滑動軸可控制圖表中顯示的狀態數目和轉換數目。 降低滑動軸只會顯示具有最高機率的狀態和轉換。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
