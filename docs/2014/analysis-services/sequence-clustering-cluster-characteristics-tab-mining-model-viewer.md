---
title: 時序群集叢集特性索引標籤（[採礦模型檢視器]） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.characteristics.f1
ms.assetid: 3a9e8a0c-7d03-47cc-8625-e68d73a8c947
author: minewiskan
ms.author: owend
ms.openlocfilehash: f82bab25b25c8d27e1aad2e2692d9ca519c9269b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940759"
---
# <a name="sequence-clustering-cluster-characteristics-tab-mining-model-viewer"></a>時序叢集的叢集特性索引標籤 (採礦模型檢視器)
  **[Microsoft 時序叢集檢視器]** 中的 **[叢集特性]** 索引標籤提供定義時序叢集之特性的詳細清單。 這些特性可包括簡單屬性/值組以及狀態之間的轉換。  
  
 可以使用此時序叢集模型檢視，向下鑽研叢集內容，以及查看代表叢集的時序。  
  
 **如需詳細資訊，請參閱 ** [Microsoft 時序叢集演算法](data-mining/microsoft-sequence-clustering-algorithm.md)、[使用 Microsoft 時序叢集檢視器瀏覽模型](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)。  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 選擇包含在目前採礦結構中，您要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視者**  
 選擇用來瀏覽選取之採礦模型的檢視器。 可以使用自訂檢視器，或 **[Microsoft 一般內容樹狀檢視器]**。 還可以使用外掛程式檢視器 (如果有)。  
  
 **該群**  
 選擇要檢視的叢集。  
  
 **的特性\<Cluster>**  
 此資料表提供已指派給目前叢集之時序的清單 (依機率排序)。 請記住，時序基本上是一個屬性/值組，後面跟著一個或多個其他的屬性/值組。 時序及其機率的組合定義了每個叢集的特性。  
  
 例如，以購物籃分析為基礎的時序叢集模型中，一個叢集的最上層特性可能是客戶選擇促銷項目，然後在不再購買其他項目的情況下結束交易。 在試圖分析伺服器失敗的時序叢集模型中，叢集的主要特性可能是一系列高頻率錯誤事件。  
  
|值|描述|  
|-----------|-----------------|  
|**變數**|此資料行表示特性是值還是轉換。<br /><br /> 如果特性是值，則 [**變數**] 資料行會包含屬性名稱。<br /><br /> 如果特性表示狀態轉換，則 [**變數**] 資料行會包含「轉換」文字。|  
|**值**|此資料行的值取決於特性是簡單屬性/值組，還是一個表示項目或事件通用時序的狀態轉換。<br /><br /> 如果特性是值，則 [**值**] 資料行會包含狀態。<br /><br /> 如果特性表示狀態轉換，則 [**值**] 資料行會包含狀態轉換的描述。|  
|**機率**|此資料行會顯示長條，用於表示此特性 (簡單屬性/值組或狀態的某種組合) 是目前叢集之成員的相對機率。<br /><br /> 可以將滑鼠停留在長條上方，來顯示特性的頻率值。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;資料採礦模型設計工具的採礦模型檢視器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
