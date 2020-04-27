---
title: 使用增益圖測試精確度（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 822d414b-4a39-473f-80c3-53476e30655a
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 06cefcdac192b715fe843f842088456f769cdd24
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63042631"
---
# <a name="testing-accuracy-with-lift-charts-basic-data-mining-tutorial"></a>使用增益圖測試精確度 (基本資料採礦教學課程)
  在資料採礦設計師的 [**挖掘精確度圖表**] 索引標籤上，您可以計算每個模型進行預測的程度，並將每個模型的結果與其他模型的結果直接比較。 這種比較方法稱為增益*圖*。 一般來說，採礦模型的預測精確度是由「增益」(Lift) 或分類精確度所衡量。 在此教學課程中，我們只會使用增益圖。  
  
 本主題中，您將會執行下列工作：  
  
-   [選擇輸入資料](#BKMK_InputData)  
  
-   [設定精確度圖表參數](#BKMK_Selecting)  
  
##  <a name="choosing-the-input-data"></a><a name="BKMK_InputData"></a>選擇輸入資料  
 若要測試採礦模型的精確度，第一個步驟就是要選取您將用於測試的資料來源。 您將會對照測試資料來測試模型的執行效果，然後搭配外部資料來使用模型。  
  
#### <a name="to-select-the-data-set"></a>若要選取資料集  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的資料採礦設計師中，切換至 [**挖掘精確度圖表**] 索引標籤，然後選取 [**輸入選擇**] 索引標籤。  
  
2.  在 [**選取要用於精確度圖表的資料集**] 群組方塊中，選取 [**使用採礦結構測試案例**]。 這是您在建立採礦結構時擱置在一旁的測試資料。  
  
     如需其他選項的詳細資訊，請參閱[選擇精確度圖表類型和設定圖表選項](../../2014/analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)。  
  
##  <a name="setting-accuracy-chart-parameters"></a><a name="BKMK_Selecting"></a>設定精確度圖表參數  
 若要建立精確度圖表，您必須定義三件事：  
  
-   精確度圖表中應該納入哪些模型？  
  
-   您要測量哪些可預測屬性？ 某些模型可能會有多個目標，但是每個圖表一次只能測量一項結果。  
  
     若要使用資料行做為精確度圖表中的**可預測資料行名稱**，這些資料行的使用`Predict`類型`Predict Only`必須是或。 此外，目標資料行的內容類型必須為 `Discrete` 或 `Discretized`。 換句話說，您無法使用增益圖測量連續數值輸出的精確度。  
  
-   您要測量模型的一般精確度，或其預測特定值的精確度（例如 [自行車購買者] = [是]）  
  
#### <a name="to-generate-the-lift-chart"></a>產生增益圖  
  
1.  在資料採礦設計師的 [**輸入選擇**] 索引標籤上，于 [**選取可預測的採礦模型資料行以顯示在增益圖中**] 底下，選取 [**同步處理預測資料行和值**] 核取方塊。  
  
2.  在 [**可預測的資料行名稱**] 資料行中，確認已為每個模型選取 [**自行車購買**者]。  
  
3.  在 [**顯示**] 資料行中，選取每個模型。  
  
     依預設，會選取採礦結構中所有的模型。 您可以決定不加入某個模型，但在本教學課程中，則是維持選取所有模型。  
  
4.  在 [**預測值**] 資料行中，選取 [ **1**]。 系統會針對具有相同可預測資料行的每個模型，自動填入相同的值。  
  
5.  選取 [增益**圖**] 索引標籤。  
  
     當您按一下此索引標籤時，預測查詢會隨即執行以取得測試資料的預測，且結果將與已知值做比較。 結果會繪製在圖形上。  
  
     如果您使用 [**預測值**] 選項來指定特定的目標結果，增益圖就會繪製隨機猜測的結果和理想模型的結果。  
  
    -   隨機猜測線條將顯示模型在沒有使用任何資料做預測時的精確度：即兩項結果彼此間為 50-50 均分。 增益圖可協助您從視覺上了解模型的執行效益與隨機猜測相比高出多少。  
  
    -   理想模型線條代表精確度的上限。 此線條顯示了當模型始終都能準確預測時，可能達到的最大效益。  
  
     您所建立的採礦模型通常會介於這兩種極端之間。 隨機猜測的任何改進*都會被視為增益。*  
  
6.  使用圖例可找出代表理想的模型與隨機猜測模型的有色線條。  
  
     您會發現`TM_Decision_Tree`模型提供最大增益，同時其效果優於群集和貝氏貝氏機率分類模型。  
  
 如需類似于此課程中所建立之增益圖的深入說明，請參閱增益[圖 &#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [&#40;基本資料採礦教學課程中測試篩選過的模型&#41;](../../2014/tutorials/testing-a-filtered-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [增益圖 &#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [增益圖索引標籤 &#40;&#41;的 [挖掘準確度] 圖表視圖](../../2014/analysis-services/lift-chart-tab-mining-accuracy-chart-view.md)  
  
  
