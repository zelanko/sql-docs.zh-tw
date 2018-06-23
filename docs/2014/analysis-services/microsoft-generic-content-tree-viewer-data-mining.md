---
title: Microsoft 一般內容樹狀檢視器 （資料採礦） |Microsoft 文件
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
- sql12.dm.miningmodeleditor.contentviewer.f1
ms.assetid: 751b4393-f6fd-48c1-bcef-bdca589ce34c
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: eb48d0ce455c41f6e684b54af86bb6ff5f8eddfb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034875"
---
# <a name="microsoft-generic-content-tree-viewer-data-mining"></a>Microsoft 一般內容樹狀檢視器 (資料採礦)
  **[Microsoft 一般內容樹狀檢視器]** 會以標準 HTML 資料表格式來顯示資料採礦模式內容的詳細資訊。 此檢視很有用，因為它會公開模型的基礎結構，以及有關係數、值分佈等項目的詳細資料。  
  
 資料表中顯示的實際內容會依照使用的演算法而變更，可能包含資料行、規則、屬性 (Property)、屬性 (Attribute)、節點和公式。 如需模型內容以及如何解譯每個模型類型之資訊的詳細資訊，請參閱[採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
 檢視器中顯示的資訊會使用以採礦模型的內容結構描述資料列集為基礎的通用結構。 內容結構描述資料列集是一般架構，可用來儲存資料採礦模型的模式、統計資料和其他內容。 如需採礦模型的資料採礦結構描述資料列集中的資料行清單，請參閱 [DMSCHEMA_MINING_MODEL_CONTENT 資料列集](schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)。  
  
## <a name="options"></a>選項。  
 **節點標題 (唯一 ID)**  
 此窗格顯示所選採礦模型中所有節點的清單。 樹狀目錄中排列節點的方式根據要檢視的模型類型而不同。  
  
 您可以按一下每個節點，以在 **[節點詳細資料]** 窗格中顯示有關節點的詳細資料。  
  
 **節點詳細資料**  
 顯示有關選取之節點內容的詳細資訊。 每個節點都會以標準化格式儲存其資訊，但資料表中每行的內容和精確度取決於要檢視的模型類型或節點類型。 例如，針對表示關聯模型中之規則的節點和表示決策樹模型中之樹狀目錄的節點所儲存的資訊不同。  
  
 如需如何解譯特定模型類型之節點資訊的相關資訊，請參閱[採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦查詢](data-mining/data-mining-queries.md)  
  
  