---
title: 流覽預測模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- forecasting [data mining]
- mining models, viewing
- mining model, time series
- time series [data mining]
ms.assetid: ad35a528-1949-4048-8678-3b9760c1c88c
author: minewiskan
ms.author: owend
ms.openlocfilehash: acf5d2f16271cf525194c1df48ac02c4c4241467
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527699"
---
# <a name="browsing-a-forecasting-model"></a>瀏覽預測模型
  當您使用 **[流覽]** 來開啟預測模型時，該模型會顯示在互動式檢視器中，類似于中的時間序列模型檢視器 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 此檢視器可協助您探索趨勢、比較序列、建立預測，以及取得有關模型和基礎資料的資訊。  
  
##  <a name="explore-the-model"></a><a name="bkmk_Top"></a>探索模型  
 適用于預測模型的**流覽**檢視器提供了圖表視圖，它會顯示一段時間的趨勢，並可讓您建立預測和模型視圖，將時間序列表示為決策樹或迴歸樹狀結構。  
  
-   [圖表檢視](#bkmk_charts)  
  
-   [[模型] 檢視](#bkmk_Model)  
  
 若要試驗預測模型，您可以使用範例資料活頁簿之 [預測] 索引標籤上的範例資料，並使用 [預測] Wizard 建立時間序列模型 &#40;[**資料採礦**] 功能區中的 [[適用于 Excel 的資料採礦增益集]&#41;](forecast-wizard-data-mining-add-ins-for-excel.md) ，或在 [**分析**] 功能區中[預測適用于 excel&#41;的 &#40;資料表分析工具](forecast-table-analysis-tools-for-excel.md)。  
  
###  <a name="chart"></a><a name="bkmk_charts"></a>圖  
 [**圖表**] 索引標籤會顯示一段時間內資料數列的趨勢，以及預測的值。 圖表的垂直軸代表序列的值，而水平軸代表時間。  
  
##### <a name="explore-the-forecasting-chart"></a>探索預測圖表  
  
1.  此模型包含多個時間序列，不過為了簡化圖表，您可以顯示一個序列，或只顯示幾個相關序列。  
  
     ![預測模型中的歷程記錄預測](media/dm13-forecast-chart-historicpredictions.gif "預測模型中的歷程記錄預測")  
  
     使用核取方塊只選取北美洲的銷售量預測。  
  
2.  按一下 [**預測步驟**] 並輸入新的值，以控制您想要在圖表中看到多少未來時間值。  
  
     預設值為 5。  
  
3.  按一下 [歷程記錄] 或 [未來] 這一行中的任何一點，以查看該時間點的確切值（顯示在 [**挖掘圖例**] 中）。  
  
4.  圖表會顯示記錄資料和未來的資料。 注意套用陰影效果背景的虛線。 這些值是根據模型的未來預測。  
  
     圖表左側顯示用來建立模型的記錄資料。  
  
5.  選取 [**顯示歷史預測**] 選項，以瞭解時間序列的穩定性。  
  
     ![模型中單一數列的預測](media/dm13-forecast-chart-singleseries.gif "模型中單一數列的預測")  
  
     記錄預測是根據該點的序列所預測的值，會與實際記錄值進行比較。 如果虛線 (預測值) 與實心線條 (實際值) 相差很多，表示序列的第一部分可能無法正確地預測稍後的值。 您可能需要更多資料，這也可能只是指出循環的變動性。  
  
6.  選取 [**顯示偏差**] 選項，以在圖表中顯示誤差線。  
  
     誤差線可讓您以視覺化方式評估預測的變化性。 預測的品質視您的來源資料而有所不同，但是隨著您增加預測步驟的數目，您應該會看到偏差穩定地增加。  
  
 **提示**  
  
-   若要切換 [**挖掘圖例**] 的顯示，請以滑鼠右鍵按一下圖表中的任一點。  
  
     您可以按一下圖表，在圖表上拖曳時間選取範圍，然後再按一下圖表在選取的範圍上放大，以檢視特定的時間範圍。  
  
-   若要取得目前圖表的複本，請按一下 [**複製到 excel**]，然後按一下 excel 中的工作表。 即會使用您已設定的所有選項 (包括圖例) 將圖表插入工作表。  
  
     不過，此圖形是靜態的，因此您無法編輯圖例或查看基礎資料。如果您需要更互動式的圖表視圖，請使用[Visio viewer](viewing-data-mining-models-in-visio-data-mining-add-ins.md)。  
  
-   按一下檢視器功能表列中的 [ **Abs** ]，在絕對與相對曲線之間切換。  
  
     如果圖表包含多個模型，但每一個模型的資料比例差異很大，則此選項會很有用。  
  
     例如，如果太平洋地區商店是新開的商店但銷售量很低，此時若使用絕對值，顯示太平洋地區銷售量的線條可能會很扁平，而難以查看實際變更，至於其他模型則以較為正常的比例顯示。  
  
     藉由將檢視切換為使用相對值，您可以標準化不同模型的比例，並將差異顯示為變動百分比。 當變動與每個模型相關時，則可以在相同的圖表中顯示，而不會大幅失真。  
  
 [探索模型](#bkmk_Top)  
  
###  <a name="model"></a><a name="bkmk_Model"></a>模組  
 預測模型也可以決策樹來表示，如果序列大部分呈線性，則可以迴歸模型來表示。  
  
 例如，在此模型中，根據特定條件迴歸公式含有差異，因此會將樹狀結構分成兩個分支，每個分支使用不同的迴歸公式。  
  
 ![在預測模型中篩選單一數列](media/dm13-forecast-model-northamerica.gif "在預測模型中篩選單一數列")  
  
##### <a name="explore-the-forecasting-model-as-a-tree"></a>探索樹狀結構的預測模型  
  
1.  按一下 [**樹狀**] 下拉式清單，然後選擇要顯示的模型。  
  
     每個可預測的屬性會顯示不同的樹狀結構或迴歸節點。 例如，如果您的資料包含歐洲、北美洲和太平洋地區的銷售量，則會有三個模型，每個模型各代表一個資料數列。  
  
2.  拖曳 [**顯示層級**] 滑杆以篩選出較低層級的樹狀結構，並將焦點放在最重要的分割上。  
  
3.  按一下每個節點，即可在 [**挖掘圖例**] 中查看一些描述性統計資料。  
  
     當您將滑鼠暫停在某個節點上方時，[工具提示] 也會顯示相同的統計資料，以及描述該節點的完整公式。  
  
4.  如果您想要複製 [**挖掘圖例**] 中的資訊，請以滑鼠右鍵按一下 [**挖掘圖例**]，選取 [**複製**]，然後在您的 Excel 工作表內按一下。 [**複製到 Excel** ] 選項會複製圖形，而不是統計資料。  
  
 [探索模型](#bkmk_Top)  
  
## <a name="see-also"></a>另請參閱  
 [在 Excel 中流覽模型 &#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
