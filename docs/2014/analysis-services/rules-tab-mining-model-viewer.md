---
title: 規則索引標籤（[採礦模型檢視器]） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.associationrules.rules.f1
ms.assetid: 705d5492-b58f-45d9-94d7-ed57b7025823
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fca78578046122a1598df096e45965367b7880ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070094"
---
# <a name="rules-tab-mining-model-viewer"></a>規則索引標籤 (採礦模型檢視器)
  在關聯模型中使用 [規則]**** 窗格，即可檢視演算法從資料擷取的規則。 規則描述各項目之間相互關聯的方式，可用於建立建議。  
  
 您可以使用檢視器中的選項來篩選檢視器所顯示的規則數目。  
  
> [!WARNING]  
>  根據預設，檢視器只顯示高於 [最小機率]**** 中定義之機率臨界值的規則。 無法使用檢視器減小此值，因為規則輸出的機率臨界值是在建立模型時決定的。 如需詳細資訊，請參閱 [Microsoft 關聯分析演算法技術參考](data-mining/microsoft-association-algorithm-technical-reference.md)。  
  
 **如需詳細資訊：** [Microsoft 關聯分析演算法](data-mining/microsoft-association-algorithm.md)、[使用 microsoft 關聯規則檢視器流覽模型](data-mining/browse-a-model-using-the-microsoft-association-rules-viewer.md)  
  
## <a name="options"></a>選項。  
 **重新整理檢視器內容**  
 在檢視器中重新載入採礦模型。  
  
 **採礦模型**  
 選擇包含在目前採礦結構中，您要檢視的採礦模型。 採礦模型會在其關聯的檢視器中開啟。  
  
 **檢視器**  
 選擇用來檢視選取之採礦模型的檢視器。 可以使用每個採礦模型的自訂檢視器，或 [Microsoft 一般內容樹狀檢視器]****。 還可以使用外掛程式檢視器 (如果有)。  
  
 **最小機率**  
 變更此值可設定在檢視器中顯示規則所需的最小機率。 增大機率值會減少顯示的規則數目。  
  
 **最低重要性**  
 變更此值可設定在檢視器中顯示規則所需的最低重要性。 增大重要性值會減少顯示的規則數目。  
  
 **篩選規則**  
 輸入字串值，即可篩選在檢視器中出現的規則數目。  
  
 還可以輸入 .NET 規則運算式做為篩選準則。 例如，下列運算式會傳回規則左側包含 'Road Bottle Cage' 的所有規則：  
  
 `\bRoad\b.\bBottle\b.\bCage\b.*->.*`  
  
 請注意，您可能需要重新整理檢視，才能查看篩選準則套用情況。 您也可以開啟和關閉 [顯示完整名稱]**** 選項以重新整理清單。  
  
 根據預設，篩選準則會套用至屬性/值組合的完整名稱；因此，如果您只檢視屬性名稱，則可能無法明確知道已正確套用篩選準則。 使用 [顯示]**** 下拉式清單可選取 [顯示屬性名稱和值]****，並驗證是否已正確篩選項目集的清單。  
  
 **顯示**  
 調整在檢視器中顯示規則的方式。 您可以選取下列三個選項之一：  
  
-   顯示屬性名稱和值  
  
-   只顯示屬性值  
  
-   只顯示屬性名稱  
  
 **顯示完整名稱**  
 按照規則出現在採礦模型內容的情形來顯示規則的完整名稱。  
  
 **最大資料列數**  
 限制檢視器中顯示的規則數目。  
  
 **機率**  
 此資料行在圖表中顯示每個規則的機率。  
  
 您可以按一下資料行標題，依機率來排序。  
  
 **重要性**  
 此資料行在圖表中顯示每個規則的重要性。  
  
 您可以按一下資料行標題，依重要性來排序。  
  
 **規則**  
 依據使用 [顯示]**** 和 [顯示完整名稱]**** 選項指定的格式，此資料行在圖表中顯示每個規則的文字說明。  
  
 您可以按一下資料行標題，依規則文字來排序。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [&#40;資料採礦模型設計工具的採礦模型檢視器&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [資料採礦模型檢視器](data-mining/data-mining-model-viewers.md)  
  
  
