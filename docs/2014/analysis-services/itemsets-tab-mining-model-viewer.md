---
title: 項目集 索引標籤 （採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.itemsets.f1
ms.assetid: 95b2b805-b142-4064-9c80-4b1b3fe2fe63
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b34031f0554fd9743ba036c9ce0f1bebe2c3d44d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079563"
---
# <a name="itemsets-tab-mining-model-viewer"></a>項目集索引標籤 (採礦模型檢視器)
  您可以使用 [項目集] 窗格，檢視關聯規則採礦模型所包含的常見項目集。 因為關聯模型可包含許多項目集，所以檢視器中提供了一些控制項，協助您篩選在檢視器中顯示的項目集。  
  
 **如需詳細資訊：**[Microsoft 關聯分析演算法](data-mining/microsoft-association-algorithm.md)，[瀏覽模型，使用 Microsoft 關聯規則檢視器](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>選項  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 選擇包含在目前採礦結構中，您要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **Viewer**  
 選擇用來檢視選取之採礦模型的檢視器。 可以使用自訂的關聯模型檢視器，或 [ [!INCLUDE[msCoName](../includes/msconame-md.md)] 一般內容樹狀檢視器]。 還可以使用外掛程式檢視器 (如果有)。  
  
 **最小支援**  
 變更此值以設定項目集必須包含的最小支援，才能出現在檢視器中。 首次開啟模型時顯示的預設值是由模型所計算，但您可以變更此值以查看更多或更少項目集。  
  
 **最小的項目集大小**  
 變更此值可設定項目集必須包含的最小項目數目，才能出現在檢視器中。  
  
 **篩選項目集**  
 輸入字串值，即可篩選在檢視器中出現的項目集數目。  
  
 還可以輸入 .NET 規則運算式做為篩選準則。 例如，下列運算式會傳回包含 'Road Bottle Cage' 的所有項目集：  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*`  
  
 請注意，您可能需要重新整理檢視，才能查看篩選準則套用情況。 您也可以開啟和關閉 [顯示完整名稱] 選項以重新整理清單。  
  
 根據預設，篩選準則會套用至屬性/值組合的完整名稱；因此，如果您只檢視屬性名稱，則可能無法明確知道已正確套用篩選準則。 使用 [顯示] 下拉式清單可選取 [顯示屬性名稱和值]，並驗證是否已正確篩選項目集的清單。  
  
 **顯示**  
 調整在檢視器中顯示項目集的方式。 您可以選取下列三個選項之一：  
  
-   顯示屬性名稱和值  
  
-   只顯示屬性值  
  
-   只顯示屬性名稱  
  
 請注意，此選項不會重新查詢模型；它只篩選所顯示的屬性或值。  
  
 **顯示完整名稱**  
 選取此選項可顯示項目集在採礦模型內容中的完整名稱。  
  
 **最大資料列**  
 限制在檢視器中顯示的項目集數目。 根據預設，項目集是依支援的遞減順序排序，因此，減小此值會限制清單，只列出最常用的項目集。  
  
 **支援**  
 顯示對每個項目集的支援。  
  
 **大小**  
 顯示存在於每個項目集內的項目數目。  
  
 **Itemset**  
 顯示每個項目集的描述。 根據預設，項目集表示為以逗號分隔的屬性及其值清單。 您可以使用 [顯示] 選項來變更其顯示方式。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器 &#40;資料採礦模型設計師&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
