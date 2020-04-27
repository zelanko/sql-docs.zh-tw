---
title: 類神經網路（採礦模型檢視器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.neuralnet.f1
ms.assetid: 18d87e7b-a821-40ea-9bd8-c6fecf189a1c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 05654d9206f09d151abd5557d0aa6aae90b1b9ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072322"
---
# <a name="neural-network-mining-model-viewer"></a>類神經網路 (採礦模型檢視器)
  使用 **[類神經網路]** 檢視器，即可探索以 [!INCLUDE[msCoName](../includes/msconame-md.md)] 類神經網路演算法或 [!INCLUDE[msCoName](../includes/msconame-md.md)] 羅吉斯迴歸演算法為基礎的採礦模型。  
  
 **如需詳細資訊，請參閱 ** [Microsoft 類神經網路演算法](data-mining/microsoft-neural-network-algorithm.md)、[Microsoft 羅吉斯迴歸演算法](data-mining/microsoft-logistic-regression-algorithm.md)、[使用 Microsoft 類神經網路檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 在目前採礦結構中選擇要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視器**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用自訂檢視器，或 **[Microsoft 一般內容樹狀檢視器]**。 還可以使用外掛程式檢視器 (如果有)。  
  
 **輸入**  
 使用此區域選擇輸入屬性和值，以便您稍後可以探索它們如何影響結果。  
  
|值|描述|  
|-----------|-----------------|  
|**屬性**|從清單選擇輸入屬性。 如果您將選取專案保留為預設值 [ ** \<所有>**]，則圖表會顯示所有輸入屬性的清單，並依其對可預測屬性的影響進行排序。|  
|**ReplTest1**|選擇輸入屬性的值。|  
  
 **輸出**  
 使用這些控制項，選擇要在橫條圖中分析和比較的可預測屬性和值。 如果您未變更選取項目，則橫條圖會比較最上面的兩個結果狀態。  
  
|值|描述|  
|-----------|-----------------|  
|**輸出屬性**|選擇可預測屬性。 如果您在建立模型時未將資料行定義為可預測資料行，則無法在此處新增它。|  
|**值 1**|選擇一種可預測屬性狀態，和 **[值 2]** 裡包含的狀態進行比較。<br /><br /> 可以比較任兩個離散或離散化值；但無法像在其他檢視器中一樣，比較值與其補數。|  
|**值2**|選取一種可預測屬性狀態，和 **[值 1]** 裡包含的狀態進行比較。|  
  
 **變數**  
 [類神經網路]**** 索引標籤的此部分包含互動式橫條圖，該圖會對您選擇的輸入和結果屬性進行回應。 因為類神經網路會計算某個特定值影響特定結果的可能性，所以您可以選擇任何輸入組合，橫條圖就會顯示該組合如何影響一組要比較的結果。  
  
|值|描述|  
|-----------|-----------------|  
|**屬性**|顯示您在 **[屬性]** 中所選取輸入屬性的名稱。|  
|**ReplTest1**|顯示所選取輸入屬性的值。|  
|**偏好\<值 1>**|顯示長條，該圖表示此特定屬性/值組合對 [值 1]**** 中選擇的目標結果有多大影響。|  
|**偏好\<值 2>**|顯示長條，該圖表示此特定屬性/值組合對 [值 2]**** 中選擇的目標結果有多大影響。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;資料採礦模型設計工具的採礦模型檢視器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
