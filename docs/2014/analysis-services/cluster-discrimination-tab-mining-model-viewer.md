---
title: 叢集辨識索引標籤 （採礦模型檢視器） |Microsoft 文件
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
- sql12.dm.miningmodeleditor.clustering.discrimination.f1
ms.assetid: ae7cfff7-ab1c-4cf5-9a91-97b21d15d85f
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8c23aeea11db212ce065baa04d5fc38280fe26a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144840"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>叢集辨識索引標籤 (採礦模型檢視器)
  使用 [叢集辨識] 索引標籤，即可比較存在於一個叢集模型中的兩個叢集。 可以查看屬性和值的不同組合在叢集中的表示方式。  
  
 **如需詳細資訊，請參閱** [Microsoft 叢集演算法](data-mining/microsoft-clustering-algorithm.md)、 [使用 Microsoft 叢集檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 在目前採礦結構中選擇採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視器**  
 選擇用來瀏覽選取之採礦模型的檢視器。 您可以使用自訂的叢集模型檢視器，或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 採礦內容檢視器。 還可以使用外掛程式檢視器 (如果有)。  
  
 **叢集 1**  
 選取叢集，以便與另一個叢集進行比較。  
  
 **叢集 2**  
 從採礦模型中的叢集清單選取第二個叢集，以便與 [叢集 1] 比較。 還可以將叢集與其補數 (表示模型中不屬於所選叢集的所有案例) 進行比較。  
  
 **辨識分數\<群集 1 > 和\<cluster 2 >**  
 圖形中的資料行提供有關每個屬性/值組與兩個選定叢集之間如何相關的資訊。  
  
|||  
|-|-|  
|**變數**|採礦模型中的屬性。|  
|**值**|[變數] 中所選屬性的值。|  
|**喜好\<群集 1 >**|左側的橫條圖表示所選屬性/值組代表 [叢集 1] 中所選叢集的機率。 將滑鼠暫時放在長條上方，可查看以百分比表示的值。 請注意，即使值為零，但這不表示叢集中必定缺少屬性/值，只不過分佈會強烈喜好其中一個叢集。|  
|**喜好\<cluster 2 >**|右側的橫條圖表示所選屬性/值組代表 [叢集 2] 中所選叢集的機率。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  