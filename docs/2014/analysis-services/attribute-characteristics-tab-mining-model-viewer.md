---
title: 屬性特性索引標籤 （採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.naivebayse.characteristics.f1
ms.assetid: f0c3350d-84c0-4ab8-9fb8-1527c2647299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 724ac86a4566bac4647e8e7358608c0f5e4ccd85
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48195608"
---
# <a name="attribute-characteristics-tab-mining-model-viewer"></a>屬性特性索引標籤 (採礦模型檢視器)
  可以使用 [屬性特性] 窗格，瀏覽貝氏機率分類模型中結果和輸入屬性之間的關聯性。 可以選擇目標屬性的值，然後查看對結果造成最大影響的輸入屬性的清單。  
  
 **如需詳細資訊，請參閱** [Microsoft 貝氏機率分類演算法](data-mining/microsoft-naive-bayes-algorithm.md)、[使用 Microsoft 貝氏機率分類檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)。  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 在目前採礦結構中選擇要檢視的採礦模型。 採礦模型會自動在最適合所選特定模型類型的自訂檢視器中開啟。  
  
 **檢視器**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以為每個模型選擇自訂檢視器，或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 採礦內容檢視器。 此清單中也會出現外掛程式檢視器 (如果有)。  
  
 **Attribute**  
 選擇要分析的可預測屬性。  
  
 **值**  
 選擇 [屬性] 中設定之可預測屬性的狀態。 因為貝氏機率分類模型不支援連續變數，所以所有目標屬性都有離散或離散化結果。 永遠會自動將遺漏屬性新增至清單。  
  
 **特性\<可預測的狀態 >**  
 圖形包含下列資料行，其中描述輸入屬性的狀態與選取之可預測屬性狀態如何相關。  
  
|值|描述|  
|-----------|-----------------|  
|**變數**|列出採礦模型中的輸入屬性。|  
|**值**|列出 [變數] 中輸入屬性的每個狀態。|  
|**機率**|長條表示該資料列中的屬性和值與可預測屬性之選取狀態相關聯的機率。 將滑鼠停留在長條上方，可查看以百分比表示的機率。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
