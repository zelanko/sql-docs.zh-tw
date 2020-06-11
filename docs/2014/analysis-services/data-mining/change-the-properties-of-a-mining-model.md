---
title: 變更採礦模型的屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], properties
- properties [data mining]
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 44313ce14beee0390f12ed0e6566502327b17795
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525034"
---
# <a name="change-the-properties-of-a-mining-model"></a>變更採礦模型的屬性
  有些採礦模型屬性可套用至整個模型，有些模型屬性只套用至個別資料行。 例如，`Drillthrough` 屬性可套用至整個模型，它指定案例資料是否應該可用於查詢，`Description` 屬性也是這類屬性。 套用至資料行的屬性包含 `Usage` 和 `ModelingFlags`，它們控制資料行中的資料在模型內的使用方式。  
  
 下列模型屬性具有可用於建立運算式或設定複雜模型屬性的進階編輯器。 下列屬性提供：  
  
-   `Filter`屬性：開啟 [[資料集篩選器] 或 [模型篩選器] 對話方塊](../data-set-filter-or-model-filter-dialog-box.md)。  
  
-   `AlgorithmParameters`屬性：開啟 [[演算法參數] 對話方塊 &#40;[採礦模型] View&#41;](../algorithm-parameters-dialog-box-mining-models-view.md)。  
  
 如需如何在採礦模型中設定屬性的資訊，請參閱 [採礦模型資料行](mining-model-columns.md)。  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>若要變更採礦模型的屬性  
  
1.  在資料採礦設計師的 [採礦模型]**** 索引標籤中，以滑鼠右鍵按一下包含採礦模型名稱的資料行標題，或方格中包含採礦演算法名稱的資料列，然後選取 [屬性]****。  
  
2.  在畫面右側的 [屬性]**** 視窗中，反白顯示對應到您要變更之屬性的值，然後輸入新值。  
  
     您在設計師中選取其他元素時，新值就會生效。  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>變更採礦模型資料行的屬性  
  
1.  在資料採礦設計師的 [採礦模型]**** 索引標籤中，以滑鼠右鍵按一下採礦結構資料行和採礦模型交集方格中的資料格，然後選取 [屬性]****。  
  
2.  在畫面右側的 [屬性]**** 視窗中，反白顯示對應到您要變更之屬性的值，然後輸入新值。  
  
    > [!NOTE]  
    >  如果 [資料行使用方式] 設定為，則資料 `Ignore` 行的 [**屬性**] 視窗是空白的。  
  
     您在設計師中選取其他元素時，新值就會生效。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型工作和使用說明](mining-model-tasks-and-how-tos.md)  
  
  
