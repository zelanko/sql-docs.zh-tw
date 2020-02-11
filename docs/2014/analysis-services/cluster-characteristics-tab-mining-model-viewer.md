---
title: 群集特性索引標籤（採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.characteristics.f1
ms.assetid: 8e33ed1d-1ce4-405d-895b-7e995b2c910d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0b4a798f9a395741ae831d3b22fc06a71f55607
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087984"
---
# <a name="cluster-characteristics-tab-mining-model-viewer"></a>叢集特性索引標籤 (採礦模型檢視器)
  [叢集特性]**** 索引標籤可讓您瀏覽叢集模型中某個叢集的特性，或瀏覽該模型中所有案例集合的特性。 圖形會將每個屬性/值組的重要性顯示為定義叢集的特性 (相較於其他叢集)。  
  
 **如需詳細資訊：** [microsoft 群集演算法](data-mining/microsoft-clustering-algorithm.md)、[使用 Microsoft 叢集檢視器流覽模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 在目前採礦結構中選擇採礦模型。 採礦模型會在自訂檢視器中開啟。  
  
 **檢視器**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用與此模型類型關聯的自訂檢視器，或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 採礦內容檢視器。 還可以使用任何可用的外掛程式檢視器。  
  
 **叢集**  
 選擇要查看的叢集，或選擇 [母體擴展 (全部)]**** 以查看模型屬性的整體分佈情況。  
  
 **叢集>\<的特性**  
 圖形包含描述所選取叢集之特性的下列資料行。  
  
|值|描述|  
|-----------|-----------------|  
|**變數**|列出在所選叢集中找到的採礦模型屬性。|  
|**值**|列出在目前所選叢集中找到的目前屬性的值。|  
|**機率**|長條表示屬性/值組做為此叢集的辨別特性的強度。 如果您將滑鼠停留在長條上方，則可查看以百分比表示的機率值。 這表示，在任何特定案例中使用此屬性和值組合時，該案例會屬於此叢集的機率。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;資料採礦模型設計工具的採礦模型檢視器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
