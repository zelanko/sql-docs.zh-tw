---
title: "分類矩陣 (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- displaying mining accuracy
- confusion matrix [data mining]
- classification matrix [Analysis Services]
- accuracy testing [data mining]
ms.assetid: 5c12f202-2ed9-41fa-bee2-0f7ab3ff058a
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8882fb1235b4d8beeb819833c76c872f1a4df76f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="classification-matrix-analysis-services---data-mining"></a>分類矩陣 (Analysis Services - 資料採礦)
  「分類矩陣」會透過判斷預測值是否符合實際值，將模型中的所有案例分類到不同的類別目錄。 每個類別目錄中的所有案例都會計算在內，而且總數會顯示在矩陣中。 分類矩陣是統計模型評估的標準工具，有時稱為「混淆矩陣」。  
  
 您選擇 [分類矩陣] 選項時所建立的圖表，會比較實際值與您指定之每個預測狀態的預測值。 矩陣的資料列代表模型的預測值，而資料行則代表實際值。 用於分析的類別目錄包括「誤判」、「真肯定」、「誤否定」和「真否定」  
  
 分類矩陣是評估預測結果的重要工具，因為此工具可讓您容易了解及說明錯誤預測的影響。 透過檢視此矩陣之每個資料格中的數量和百分比，您可以快速查看模型正確預測的頻率。  
  
 本節將說明如何建立分類矩陣及如何解譯結果。  
  
## <a name="understanding-the-classification-matrix"></a>了解分類矩陣  
 將您建立的模型視為資料採礦基本教學課程的一部分。 [TM_DecisionTree] 模型可用來協助建立目標郵寄促銷活動，並可用來預測哪些客戶最有可能購買自行車。 若要測試此模型的預期效用，您可以使用內含已知 [Bike Buyer] 結果屬性值的資料集。 一般來說，您會使用當您建立用於定型此模型的採礦結構時所擱置在一旁的測試資料集。  
  
 只有兩種可能的結果：[是] \(客戶可能購買自行車) 及 [否] \(客戶可能不購買自行車)。 因此，產生的分類矩陣是比較簡單的。  
  
## <a name="interpreting-the-results"></a>解譯結果  
 下表顯示 TM_DecisionTree 模型的分類矩陣。 請記住，此可預測的屬性若為 0，則表示 [否]；若為 1，則表示 [是]。  
  
|預測的|0 (實際值)|1 (實際值)|  
|---------------|------------------|------------------|  
|0|362|144|  
|1|121|373|  
  
 第一個結果資料格包含 362 的值，表示值 0 的「真肯定」數目。 由於 0 表示客戶未購買自行車，所以這個統計資料告訴您，此模型在 362 個案例中預測出非自行車買主的正確值。  
  
 該資料格正下方的資料格包含 121 的值，也就告訴您「誤判」的數目，或是此模型預測某個人會購買自行車，但實際上卻沒有的次數。  
  
 包含 144 值的資料格，表示值 1 的「誤判」數目。 由於 1 表示客戶已購買自行車，所以這個統計資料告訴您，此模型在 144 個案例中預測出某個人不會購買自行車，但實際上卻有購買的次數。  
  
 最後，包含 373 值的資料格，表示目標值 1 的「真肯定」數目。 換句話說，此模型在 373 個案例中，正確預測出某個人會購買自行車。  
  
 藉由彙總對角線上相鄰之資料格中的值，就可以判斷此模型的整體精確度。 一條對角線會告訴您正確預測的總數，而其他對角線則告訴您錯誤預測的總數。  
  
### <a name="using-multiple-predictable-values"></a>使用多個可預測的值  
 [Bike Buyer] 案例特別容易解譯，因為只有兩個可能的值。 當可預測屬性有多個可能的值時，分類矩陣會針對每一個可能的實際值加入新的資料行，然後針對每一個預測值計算相符的數目。 下表顯示不同模型上的結果，其中有三個值 (0, 1, 2) 是可能的值。  
  
|預測的|0 (實際值)|1 (實際值)|2 (實際值)|  
|---------------|------------------|------------------|------------------|  
|0|111|3|5|  
|1|2|123|17|  
|2|19|0|20|  
  
 雖然加入多個資料行會讓報表看起來更為複雜，但是當您想要評估做出錯誤預測的累計成本時，其他詳細資料可能會非常實用。 若要建立對角線上的總和或是比較不同資料列組合的結果，您可以按一下 [分類矩陣] 索引標籤上提供的 [複製] 按鈕，並將報表貼到 Excel。 或者，您可以使用類似適用於 Excel 的資料採礦用戶端的用戶端 (它支援 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本)，直接在 Excel 中建立包含計數和百分比的分類報表。 如需詳細資訊，請參閱 [SQL Server Data Mining](http://go.microsoft.com/fwlink/?LinkID=77733)(SQL Server 資料採礦)。  
  
## <a name="restrictions-on-the-classification-matrix"></a>分類矩陣的限制  
 分類矩陣只能搭配離散的可預測屬性一起使用。  
  
 當您在 [採礦精確度圖表] 設計師的 [輸入選擇] 索引標籤上選取模型時，雖然可以加入多個模型，但是 [分類矩陣] 索引標籤會顯示每個模型的個別矩陣。  
  
## <a name="related-content"></a>相關內容  
 下列主題包含您可以如何建立及使用分類矩陣及其他圖表的詳細資訊。  
  
|主題|連結|  
|------------|-----------|  
|提供如何為此目標郵寄模型建立增益圖的逐步解說。|[資料採礦基本教學課程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)<br /><br /> [使用增益圖測試精確度 &#40;基本資料採礦教學課程&#41;](http://msdn.microsoft.com/library/822d414b-4a39-473f-80c3-53476e30655a)|  
|說明相關的圖表類型。|[增益圖 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [收益圖 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [散佈圖 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|描述採礦模型和採礦結構的交叉驗證用法。|[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|描述建立增益圖及其他精確度圖表的步驟。|[測試及驗證工作與操作方法 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
