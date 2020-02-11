---
title: 群集設定檔索引標籤（採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.profiles.f1
ms.assetid: 1ebafa1f-74e9-4c05-b278-a690fa8543bd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebed4b2b7cc5c6496ab0c681450897a477e4707a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087864"
---
# <a name="cluster-profiles-tab-mining-model-viewer"></a>叢集設定檔索引標籤 (採礦模型檢視器)
  使用 **[叢集設定檔]** 索引標籤以取得演算法在叢集模型中所發現之叢集的整體檢視。 索引標籤會顯示每一個屬性，以及該屬性在每一個叢集中的分佈。  
  
 **如需詳細資訊：** [microsoft 群集演算法](data-mining/microsoft-clustering-algorithm.md)、[使用 Microsoft 叢集檢視器流覽模型](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 在目前採礦結構中選擇採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視器**  
 選擇用來檢視選取之採礦模型的檢視器。 可以使用自訂的採礦模型檢視器，或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 採礦內容檢視器。 還可以使用外掛程式檢視器 (如果有)。  
  
 **顯示圖例**  
 選取此選項可顯示圖例符號，該圖例符號會顯示檢視器中的色彩與 [狀態]**** 資料行中的值之間的對應。  
  
 **長條圖列**  
 變更此值可控制每個長條圖中包含的狀態數目。 如果狀態的總數超出您選擇要顯示的狀態，長條圖中會顯示機率最高的狀態，而其餘的狀態將會分組放入 **[其他]** 中。  
  
 **屬性**  
 列出位於叢集模型中的資料行。 每個屬性的長條圖都會顯示該屬性在演算法所識別叢集之間的分佈情形。  
  
 **狀態**  
 提供圖例符號，用於表示代表叢集的對應資料列中每個狀態的色彩，或表示連續數值分佈的菱形滑動軸。 可以使用 **[顯示圖例]** 核取方塊來顯示或隱藏此資料行。  
  
 **叢集設定檔**  
 此區段會針對模型中的每個叢集包含一個資料行。 針對每個屬性，長條圖只會顯示屬性值在該叢集中的分佈。 此圖表還包含 **[母體]** 資料行，該資料行也使用長條圖來顯示每個屬性值在模型中所有案例的分佈。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;資料採礦模型設計工具的採礦模型檢視器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
