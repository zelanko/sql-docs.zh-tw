---
title: 相依性網路 索引標籤 （採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.dependencynetwork.f1
ms.assetid: e58ce1b7-20d6-42cb-ade5-916da8471e09
caps.latest.revision: 25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 01b3535c7a6c2547bdef9a4f74956ff647f1b864
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279984"
---
# <a name="dependency-network-tab-mining-model-viewer"></a>相依性網路索引標籤 (採礦模型檢視器)
  [相依性網路] 索引標籤會提供採礦模型所包含之所有屬性的圖形檢視，並顯示這些屬性彼此相關的情況。  
  
 [相依性網路] 索引標籤用於多種類型的採礦模型，包括貝氏機率分類模型、決策樹模型和關聯模型。 如需如何在這些模型的內容中解譯 [相依性網路] 索引標籤內容的詳細資訊，請參閱下列連結：  
  
 [使用 Microsoft 樹狀檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
 [使用 Microsoft 貝氏機率分類檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)  
  
 [使用 Microsoft 關聯規則檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 在目前採礦結構中選擇要檢視的採礦模型。 採礦模型會在自訂檢視器中開啟。 用於每個模型的自訂檢視器類型是由您用來建立該模型的演算法決定。  
  
 **檢視器**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用為每個採礦模型提供的自訂檢視器，或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 採礦內容檢視器。 還可以使用外掛程式檢視器 (如果有)。 Microsoft 內容樹狀檢視器可用於所有模型，並在 HTML 資料表中表示模型內容。  
  
 **放大**  
 放大圖表，以便更詳細地查看屬性。  
  
 **縮小**  
 縮小圖表，以便查看更多屬性以及這些屬性之間的連結。  
  
 **複製圖表檢視**  
 將圖表的可見部分複製到剪貼簿。  
  
 **複製整個圖表**  
 將整個圖表複製到剪貼簿。  
  
 **連結**  
 您可以調整屬性右邊的滑動軸，來調整檢視器顯示的連結 (邊緣) 數目和節點數目。 向下拖曳滑動軸會增大臨界值，以便只顯示最強連結。 對於每種模型類型，都會使用略為不同的值來表示圖形中的連結：  
  
-   在 **決策樹** 模型中，邊緣表示連接的預測強度 (由分岔分數部分決定)。  
  
-   在 **貝氏機率分類** 模型中，兩個節點之間的連結可以是任一方向：也就是說，節點 A 可預測節點 B，反之亦然。 與邊緣關聯的分數表示連接的預測強度。  
  
-   在 **關聯模型**中，節點之間的邊緣表示連接兩個項目集之規則的重要性分數。  
  
 所有模型類型的一般規則是，連結愈強，兩個屬性之間的預測關聯性也就愈強。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
