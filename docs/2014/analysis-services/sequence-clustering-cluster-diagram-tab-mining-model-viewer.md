---
title: 時序群集群集圖表索引標籤 (採礦模型檢視器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.diagrams.f1
ms.assetid: 4b705397-9af4-4678-9eda-149bc5d762fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95763dca9e5a617e3fdc1c4d1d69b45e6679a392
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62746780"
---
# <a name="sequence-clustering-cluster-diagram-tab-mining-model-viewer"></a>時序叢集的叢集圖表索引標籤 (採礦模型檢視器)
  **[Microsoft 時序叢集檢視器]** 中的 **[叢集圖表]** 索引標籤會提供時序叢集模型所包含之所有叢集的圖形檢視。  
  
 可以使用此時序叢集模型檢視，從每個叢集鑽研至支援案例 (如果已啟用鑽研)。 還可以為叢集指派描述性名稱，以及變更陰影變數，讓值分佈一目了然。  
  
 **如需詳細資訊：**[Microsoft 時序群集演算法](data-mining/microsoft-sequence-clustering-algorithm.md)，[瀏覽模型，使用 Microsoft 時序叢集檢視器](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 選擇包含在目前採礦結構中，您要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **Viewer**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用自訂檢視器，或 **[Microsoft 一般內容樹狀檢視器]**。 還可以使用外掛程式檢視器 (如果有)。  
  
 **放大**  
 將圖表放大，以取得更詳細的叢集檢視。  
  
 **縮小**  
 將圖表縮小，以查看模型中的所有叢集。  
  
 **複製圖表檢視**  
 將圖表的可見部分複製到剪貼簿。  
  
 **複製整個圖表**  
 將整個圖表複製到剪貼簿。  
  
 **將圖表縮放至視窗大小**  
 縮小圖表，直到畫面能容納整個圖表為止。  
  
 **找不到節點**  
 使用 [尋找節點] 對話方塊可篩選圖形中的叢集，更輕鬆地尋找特定叢集。 如需詳細資訊，請參閱[尋找節點對話方塊 &#40;採礦模型檢視器&#41;](find-node-dialog-box-mining-model-viewer.md)。  
  
 請注意，在此內容中，您只能搜索叢集的名稱，而不搜索叢集中的屬性；因此，如果您已為叢集指派描述性名稱，此選項最為有用。 可以在檢視器中指派叢集名稱，方法是以滑鼠右鍵按一下每個叢集並選取 [重新命名]。  
  
 **修訂版面配置**  
 重新排序圖表中的叢集，以修訂版面配置。  
  
 **密度**  
 密度橫條圖的外觀及其包含的值取決於您在 [陰影變數] 中選取的屬性。  
  
-   如果未將任何屬性狀態選定為陰影變數，則根據預設套用至每個叢集的密度陰影表示對該叢集的支援 (相較於案例整體母體擴展)。  
  
-   如果在 **[陰影變數]** 中選取屬性，則必須同時在 **[狀態]** 中選取值。 如果您這樣做，密度橫條圖會更新為顯示此狀態的機率。 可以將滑鼠暫時放在任何個別叢集上方，查看叢集選定狀態的機率。  
  
 **陰影變數**  
 從採礦模型中選取用於設定叢集圖表陰影的屬性。  
  
 **狀態**  
 選取對應於 [陰影變數] 的狀態。 例如，如果您要檢視包含特定產品的時序，您會選取 [Product] 資料行做為 [陰影變數] 的屬性，並選取特定產品名稱做為 [狀態] 的值。  
  
 **Links**  
 圖表中的線條表示時序叢集之間的關聯。 您可以調整叢集右邊的滑動軸，來調整檢視器顯示的連結數目。 降低滑桿只顯示最強的連結。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器 &#40;資料採礦模型設計師&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
