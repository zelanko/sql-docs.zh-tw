---
title: 資料採礦設計師 |Microsoft 文件
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f14ec670668253fa9e37db9647d5ef511150816
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-designer"></a>資料採礦設計師
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  資料採礦設計師是您在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中使用採礦模型的主要環境。 您可以選取現有的採礦結構，或使用資料採礦精靈來建立新的採礦結構和採礦模型，以存取此設計師。 您可以使用資料採礦設計師來執行下列工作：  
  
-   修改一開始是由資料採礦精靈所建立的採礦結構和採礦模型。  
  
-   以現有的採礦結構為基礎來建立新模型。  
  
-   培訓及瀏覽採礦模型。  
  
-   使用精確度圖表來比較模型。  
  
-   依據採礦模型建立預測查詢。  
  
## <a name="mining-structure-tab"></a>採礦結構索引標籤  
 使用 **[採礦結構]** 索引標籤，加入資料行及修改現有採礦結構的屬性。 下列工作和主題提供有關使用採礦結構的詳細資訊：  
  
 [採礦結構 & #40;Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
 [採礦結構工作和使用說明](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>採礦模型索引標籤  
 使用 **[採礦模型]** 索引標籤來管理現有的採礦模型和建立新的模型。 採礦模型一定會以現有的採礦結構為基礎。  
  
 在 [採礦模型] 索引標籤中，您可以變更演算法類型、新增或移除與模型結構相關聯的資料行、調整演算法特有的資料行屬性、指定採礦模型資料行使用方式，以及調整與採礦模型相關聯的演算法參數。 您也可以同時處理採礦結構與所選取的模型或所有相關聯的模型。  
  
 如需有關使用採礦模型的詳細資訊，請參閱下列主題：  
  
 [採礦模型 & #40;Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
 [採礦模型的工作與操作方法](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>採礦模型檢視器索引標籤  
 使用 **[採礦模型檢視器]** 索引標籤，以視覺化方式瀏覽採礦模型。 每一個採礦模型與一個自訂檢視器相關聯，後者會顯示該模型的特定內容。 您也可以使用內容檢視器來檢視採礦模型內容。  
  
 如需有關使用資料採礦檢視器瀏覽採礦模型的詳細資訊，請參閱下列主題：  
  
 [資料採礦模型檢視器](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
 [採礦模型檢視器工作和使用說明](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>採礦精確度圖表索引標籤  
 使用 **[採礦精確度圖表]** 索引標籤來測試單一採礦模型的預測精確度，或比較採礦結構內所包含之多個採礦模型的效能。 這個索引標籤包含的工具是用來篩選資料、選取採礦模型，以及以增益圖、收益圖或分類矩陣顯示結果。  
  
 如需有關測試和驗證採礦模型的詳細資訊，請參閱下列主題：  
  
 [測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
 [測試和驗證工作及操作方式 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>採礦模型預測索引標籤  
 [採礦模型預測] 索引標籤包括預測查詢產生器，可用以建立資料採礦延伸模組 (DMX) 預測查詢。 這個索引標籤包含的工具是用來指定採礦模型和輸入資料表、將採礦模型中的資料行對應到輸入資料表中的資料行、將函數加入查詢中，以及指定每一個資料行的準則。  
  
 在設計查詢之後，您可以使用索引標籤中的不同檢視來顯示查詢的結果及手動修改查詢。 您也可以將查詢的結果儲存到資料庫中的資料表。  
  
 如需有關建立資料採礦查詢的詳細資訊，請參閱下列主題：  
  
 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)  
  
 [資料採礦查詢工作和使用說明](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
