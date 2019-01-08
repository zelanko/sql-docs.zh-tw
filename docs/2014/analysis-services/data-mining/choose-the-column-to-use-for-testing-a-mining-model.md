---
title: 選擇要用於測試採礦模型的資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- columns [data mining], predictable mining columns
- Mining Accuracy Chart [Analysis Services], columns
- predictable mining columns [Analysis Services]
ms.assetid: c6a8f23a-da21-4f31-9521-99460d624649
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 340080271318073983b29abebeab85122993b489
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540246"
---
# <a name="choose-the-column-to-use-for-testing-a-mining-model"></a>選擇用於測試採礦模型的資料行
  在您可以衡量採礦模型的精確度之前，您必須決定您想要評估哪一種結果。 大多數的資料採礦模型都會要求您至少選擇一個資料行，以便在您建立模型時當做可預測的屬性使用。 因此，當您測試模型的精確度時，您通常必須選取該屬性進行測試。  
  
 下列清單描述在選擇測試用的可預測屬性時的一些其他考量事項：  
  
-   某些類型的資料採礦模型可以預測多個屬性-例如類神經網路，可以探索多個屬性之間的關聯性。  
  
-   其他類型的採礦模型-例如群集模型-請勿不一定會有可預測的屬性。 除非群集模型擁有可預測的屬性，否則無法加以測試。  
  
-   建立散佈圖或是衡量迴歸模型的精確度需要您選擇連續可預測屬性當做結果。 在該情況下，您不能指定目標值。 如果您要建立散佈圖以外的任何項目，基礎採礦結構資料行也必須具有 [離散] 或 [離散化] 的內容類型。  
  
-   如果您選擇離散屬性當作可預測的結果，您也可以指定目標值，或是將 [預測值] 欄位保留空白。 如果您納入**預測值**，圖表只會衡量模型的有效性對於預測目標值。 如果您未指定目標結果，將會衡量此模型對於預測所有結果的精確度。  
  
-   如果您想要在單一精確度圖表中包含多個模型並加以比較，則所有模型都必須使用相同的可預測資料行。  
  
-   當您建立交叉驗證報表時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將會自動分析具有相同可預測屬性的所有模型。  
  
-   當選取 [同步處理預測資料行和值] 選項時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會自動選擇擁有相同名稱和相符之資料類型的可預測資料行。 如果您的資料行不符合這些準則，您可以關閉這個選項，並手動選擇可預測資料行。 如果您正在使用外部資料集來測試模型 (此資料集擁有的資料行與模型的資料行不同)，您可能需要進行這項處理。 但是，如果您選擇具有錯誤資料類型的資料行，您將會得到錯誤或錯誤結果。  
  
### <a name="specify-the-outcome-to-predict"></a>指定預測的結果  
  
1.  按兩下採礦結構，在資料採礦設計師中將它開啟。  
  
2.  選取 **[採礦精確度圖表]** 索引標籤。  
  
3.  選取 [輸入選擇] 索引標籤。  
  
4.  在 [輸入選擇] 索引標籤的 [可預測資料行名稱] 底下，針對併入圖表中的每個模型選取可預測資料行。  
  
     [可預測資料行名稱] 方塊中提供的採礦模型資料行只限於使用類型設定為 [預測] 或 [僅預測] 的資料行。  
  
5.  如果您要判斷模型的增益，您必須從 [預測值] 清單中選取要衡量的特定結果值。  
  
## <a name="see-also"></a>另請參閱  
 [選擇和對應模型測試資料](choose-and-map-model-testing-data.md)   
 [選擇精確度圖表類型及設定圖表選項](choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  
