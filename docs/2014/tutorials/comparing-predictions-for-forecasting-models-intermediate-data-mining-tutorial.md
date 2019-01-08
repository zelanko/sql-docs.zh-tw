---
title: 比較預測的預測模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ead8a1fe-60d8-4017-8fb8-6fe32168e46d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb208d3b19e7ca2d49198a2f57edaf48214bb78f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395371"
---
# <a name="comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial"></a>比較用來預測模型的預測 (中繼資料採礦教學課程)
  在本教學課程的先前步驟中，您建立了多個時間序列模型：  
  
-   每一個地區和模型組合的預測 (僅根據個別模型和地區的資料)。  
  
-   每個地區的預測 (根據更新的資料)。  
  
-   所有模型的全球預測 (根據彙總資料)。  
  
-   M200 模型在北美地區的預測 (根據彙總模型)。  
  
 為了概述時間序列預測的功能，您將檢閱變更，了解使用擴充或取代資料的選項如何影響預測結果。  
  
 [EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
##  <a name="bkmk_EXTEND"></a> 加入資料之後比較原始結果與結果  
 讓我們看看只是要了解如何使用新資料更新模型會影響結果的太平洋地區 M200 產品線的資料。 請記得原始資料數列在 2004 年 6 月結束，而我們取得 7 月、8 月和 9 月的新資料。  
  
-   第一個資料行顯示加入的新資料。  
  
-   第二個資料行顯示 7 月以後根據原始資料數列的預測。  
  
-   第三個資料行顯示根據擴充資料的預測。  
  
|**M200 Pacific**|更新的實際銷售資料|加入資料之前的預測|擴充預測|  
|----------------------|-----------------------------|------------------------------------|-------------------------|  
|7-25-2008|**65**|32|**65**|  
|8-25-2008|**54**|37|**54**|  
|9-25-2008|**61**|32|**61**|  
|10-25-2008|無資料|36|32|  
|11-25-2008|無資料|31|41|  
|12-25-2008|無資料|34|32|  
  
 您將會注意到使用擴充資料 (此處以粗體顯示) 的預測完全重複實際資料點。 重複是預設行為。 只要有可用的實際資料點，預測查詢就會傳回實際值，只在新的實際資料點已經用完後才會輸出新的預測值。  
  
 一般而言，相較於模型資料開頭的資料，演算法對新資料的變更賦予較重的加權。 不過，在此情況下，新銷售數字比起上一個週期增幅僅為 20-30%，因此對預計銷售造成些微的上揚，在此之後銷售預測轉而向下，重複加入新資料之前月份的趨勢。  
  
##  <a name="bkmk_REPLACE"></a> 比較原始和交叉預測結果  
 請記得，原始採礦模型揭露地區之間和產品線之間有很大的差異。 例如，M200 模型的銷售非常強，而 T1000 模型的銷售則在所有地區都很低。 此外，有些數列沒有太多資料。 序列是不完全的這表示它們不會有相同的起始點。  
  
 ![序列預測 M200 與 T1000 數量](../../2014/tutorials/media/6series-defaultforecasting.gif "序列預測 M200 與 T1000 數量")  
  
 因此，當您根據一般模型做預測，此模型以全球銷售而不是以原始資料集為基礎，預測會如何變更？ 為確保不遺失任何資訊或扭曲預測，您可以將結果儲存至資料表，將預測的資料表聯結至歷程記錄資料的資料表，然後在圖形中顯示兩組歷程記錄資料和預測。  
  
 下圖只以 M200 一個產品線為基礎。 圖形將初始採礦模型中的預測與使用彙總採礦模型的預測相比較。  
  
 ![Excel 圖表比較預測](../../2014/tutorials/media/m200-predictions-compared.gif "Excel 圖表比較預測")  
  
 您可以從此圖中得知，彙總採礦模型保留值的整體範圍和趨勢，同時將個別資料數列中的波動降至最低。  
  
## <a name="conclusion"></a>結論  
 您已經學會如何建立及自訂可用於預測的時間序列模型。  
  
 您已經學會使用 EXTEND_MODEL_CASES 參數，加入新資料及建立預測來更新時間序列模型，而不需重新處理模型。  
  
 您已經學會使用 REPLACE_MODEL_CASES 參數以及將模型套用至不同資料數列，建立可用於交叉預測的模型。  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料採礦教學課程&#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [時間序列模型查詢範例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
