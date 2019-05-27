---
title: 時序群集群集辨識索引標籤 （採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 914629fca09d4bcffb5ac931316331bbb7e7eebe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069140"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>時序叢集的叢集辨識索引標籤 (採礦模型檢視器)
  [Microsoft 時序叢集檢視器] 中的 [叢集辨識] 索引標籤可比較時序叢集模型中的選定叢集。  
  
 可以使用此時序叢集模型檢視，比較兩個叢集並查看哪些狀態和轉換是不同的。  
  
 **如需詳細資訊：**[Microsoft 時序群集演算法](data-mining/microsoft-sequence-clustering-algorithm.md)，[瀏覽模型，使用 Microsoft 時序叢集檢視器](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 選擇包含在目前採礦結構中，您要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **Viewer**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用自訂檢視器，或 **[Microsoft 一般內容樹狀檢視器]**。 還可以使用外掛程式檢視器 (如果有)。  
  
 **叢集 1**  
 在模型中選取叢集。  
  
 **叢集 2**  
 在採礦模型中選取第二個叢集來與 **叢集 1**進行比較。  
  
 如果您未選取其他叢集，則根據預設，所選叢集會與其補數 (表示模型中不屬於叢集 1 的所有案例) 進行比較。  
  
 **辨識率\<群集 1 > 和\<cluster 2 >**  
 此圖表提供所選叢集的詳細比較。 一般情況下，叢集模型很少以獨佔方式為單一叢集指派狀態或值。 因此，檢視器只表示特定屬性或狀態「喜好」某個特定叢集。  
  
 整體而言，特定叢集可能主要包含某個狀態：例如，常見狀態可能為依序購買 Water Bottle 和 Water Bottle Cage。 但是，此順序可能存在於其他有更重要定義特性的叢集中。 例如，另一個叢集的最主要特性可能是交易時間非常短，並且分析顯示，Water Bottle 和 Water Bottle Cage 項目可能通常分組到此叢集中，但並非總是這樣。  
  
|值|描述|  
|-----------|-----------------|  
|**變數**|採礦模型中的屬性。|  
|**值**|[變數] 中列出之屬性的狀態。|  
|**喜好\<群集 1 >**|包含陰影長條，表示 [變數] 和 [值] 中列出的屬性和狀態喜好 [叢集 1] 中所選叢集的強度。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器 &#40;資料採礦模型設計師&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
