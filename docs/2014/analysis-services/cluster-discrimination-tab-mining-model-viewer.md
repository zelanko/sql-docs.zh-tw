---
title: 群集辨識索引標籤（[採礦模型檢視器]） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.discrimination.f1
ms.assetid: ae7cfff7-ab1c-4cf5-9a91-97b21d15d85f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d55f61d9255d19f22fffb7380785a2ada1a2763
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087902"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>叢集辨識索引標籤 (採礦模型檢視器)
  使用 [叢集辨識]**** 索引標籤，即可比較存在於一個叢集模型中的兩個叢集。 可以查看屬性和值的不同組合在叢集中的表示方式。  
  
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
  
 **群集 2**  
 從採礦模型中的叢集清單選取第二個叢集，以便與 [叢集 1]**** 比較。 還可以將叢集與其補數 (表示模型中不屬於所選叢集的所有案例) 進行比較。  
  
 **群集 1> \<和\<叢集 2>的辨識分數**  
 圖形中的資料行提供有關每個屬性/值組與兩個選定叢集之間如何相關的資訊。  
  
|||  
|-|-|  
|**變數**|採礦模型中的屬性。|  
|**值**|[變數]**** 中所選屬性的值。|  
|**優先\<的叢集 1>**|左側的橫條圖表示所選屬性/值組代表 [叢集 1]**** 中所選叢集的機率。 將滑鼠暫時放在長條上方，可查看以百分比表示的值。 請注意，即使值為零，也不表示叢集中的屬性值不一定會遺失，只是散發會對另一個叢集進行強式比對。|  
|**\<偏好叢集 2>**|右側的橫條圖表示所選屬性/值組代表 [叢集 2]**** 中所選叢集的機率。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;資料採礦模型設計工具的採礦模型檢視器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
