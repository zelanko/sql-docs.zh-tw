---
title: 羅吉斯迴歸模型查詢範例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- content queries [DMX]
ms.assetid: 7c8e13a3-5c67-46c2-abfa-4881e6ef9c62
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d156a8f015a45ca257bf4f988cf69d229eafe5f0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66084225"
---
# <a name="logistic-regression-model-query-examples"></a>羅吉斯迴歸模型查詢範例
  當您針對資料採礦模型建立查詢時，可以建立內容查詢來提供有關分析期間所發現之模式的詳細資料，也可以建立預測查詢來使用模型中的模式，透過新的資料進行預測。  
  
 本節說明如何針對以 Microsoft 羅吉斯迴歸演算法為基礎的模型建立查詢。  
  
 **內容查詢**  
  
 [使用資料採礦結構描述資料列集擷取模型參數](#bkmk_Query1)  
  
 [使用 DMX 尋找有關模型的其他詳細資料](#bkmk_Query2)  
  
 **預測查詢**  
  
 [針對連續值進行預測](#bkmk_Query3)  
  
 [針對離散值進行預測](#bkmk_Query4)  
  
##  <a name="bkmk_top"></a> 取得有關羅吉斯迴歸模型的資訊  
 羅吉斯迴歸模型是使用 Microsoft 類神經網路演算法搭配一組特殊的參數所建立。因此，羅吉斯迴歸模型所擁有的部分資訊與類神經網路模型相同，但是較不複雜。 若要了解模型內容的結構，以及哪一種節點類型會儲存那一種資訊，請參閱 [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-logistic-regression-models.md)。  
  
 若要依照查詢案例，您可以建立羅吉斯迴歸模型，中繼資料採礦教學課程的下一節所述：[第 5 課：建立類神經網路和羅吉斯迴歸模型&#40;中繼資料採礦教學課程&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)。  
  
 您也可以使用 [資料採礦基本教學課程](../../tutorials/basic-data-mining-tutorial.md)的採礦結構：目標郵寄。  
  
```  
ALTER MINING STRUCTURE [Targeted Mailing]  
ADD MINING MODEL [TM_Logistic Regression]  
([Customer Key],  
[Age],  
[Bike Buyer] PREDICT,  
[Yearly Income] PREDICT,  
[Commute Distance],  
[English Education],  
Gender,  
[House Owner Flag],  
[Marital Status],  
[Number Cars Owned],  
[Number Children At Home],  
[Region],  
[Total Children]  
)  
USING Microsoft_Logistic_Regression  
```  
  
###  <a name="bkmk_Query1"></a> 範例查詢 1:使用資料採礦結構描述資料列集擷取模型參數  
 您可以藉由查詢資料採礦結構描述資料列集來尋找有關此模型的中繼資料，例如此模型建立的時間、上次處理此模型的時間、此模型所根據的採礦結構名稱，以及用來當做可預測屬性的資料行名稱。 下列範例會傳回第一次建立模型時所使用的參數，以及模型的名稱、類型與建立模型的日期。  
  
```  
SELECT MODEL_NAME, SERVICE_NAME, DATE_CREATED, MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center_LR'  
```  
  
 範例結果：  
  
|MODEL_NAME|SERVICE_NAME|DATE_CREATED|MINING_PARAMETERS|  
|-----------------|-------------------|-------------------|------------------------|  
|Call Center_LR|Microsoft_Logistic_Regression|04/07/2009 20:38:33|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=1, MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255, MAXIMUM_STATES=100, SAMPLE_SIZE=10000|  
  
###  <a name="bkmk_Query2"></a> 範例查詢 2:使用 DMX 尋找有關模型的其他詳細資料  
 下列查詢會傳回有關羅吉斯迴歸模型的一些基本資訊。 羅吉斯迴歸模型在許多方面類似於類神經網路模型，包括存在一個描述當做輸入使用之值的臨界統計資料節點 (NODE_TYPE = 24)。 這個範例查詢會使用目標郵寄模型，並且從巢狀資料表 NODE_DISTRIBUTION 中擷取所有輸入的值，藉以取得這些值。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM [TM_Logistic Regression].CONTENT   
```  
  
 部分結果：  
  
|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Age|Missing|0|0|0|1|  
|Age|45.43491192|17484|1|126.9544114|3|  
|Bike Buyer|Missing|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|Commute Distance|Missing|0|0|0|1|  
|Commute Distance|5-10 英哩|3033|0.173472889|0|4|  
  
 實際查詢會傳回更多資料列，但是，這個範例說明關於輸入所提供之資訊的類型。 若為離散輸入，每個可能值都會列在資料表中。 若為連續值輸入 (例如 Age)，就無法列出完整清單，因此輸入會離散化為平均值。 如需如何使用臨界統計資料節點中資訊的詳細資訊，請參閱[羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-logistic-regression-models.md)。  
  
> [!NOTE]  
>  這些結果已經過扁平化，讓檢視更為容易，但是如果您的提供者支援階層式資料列集，則可以在單一資料行中傳回巢狀資料表。  
  
## <a name="prediction-queries-on-a-logistic-regression-model"></a>羅吉斯迴歸模型的預測查詢  
 您可以搭配各種採礦模型使用 [Predict &#40;DMX&#41;](/sql/dmx/predict-dmx) 函數來提供新的資料給模型，並且根據新的值進行預測。 您也可以使用這些函數傳回關於預測的其他資訊，例如，預測正確的機率。 本節也針對羅吉斯迴歸模型，提供一些預測查詢的範例。  
  
###  <a name="bkmk_Query3"></a> 範例查詢 3:針對連續值進行預測  
 由於羅吉斯迴歸支援將連續屬性同時用於輸入和預測，因此，在資料中建立與各種因數相互關聯的模型相當容易。 您可以使用預測查詢來探索這些因數之間的關聯性。  
  
 下列查詢範例是以中繼教學課程中的撥接中心模型為基礎，並且建立單一查詢，以便預測星期五上午排班的服務等級。 [PredictHistogram (DMX)](/sql/dmx/predicthistogram-dmx) 函數會傳回一個巢狀資料表，其中提供與了解預測值之有效性相關的統計資料。  
  
```  
SELECT  
  Predict([Call Center_LR].[Service Grade]) as Predicted ServiceGrade,  
  PredictHistogram([Call Center_LR].[Service Grade]) as [Results],  
FROM  
  [Call Center_LR]  
NATURAL PREDICTION JOIN  
(SELECT 'Friday' AS [Day Of Week],  
  'AM' AS [Shift]) AS t  
```  
  
 範例結果：  
  
 **預測服務等級**:0.102601830123659  
  
 **結果**  
  
|服務等級|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.102601830123659|83.0232558139535|0.988372093023256|0|0.00120552660600087|0.034720694203902|  
||0.976744186046512|0.0116279069767442|0.0116279069767442|0|0|  
  
 如需巢狀 NODE_DISTRIBUTION 資料表之機率、支援及標準差值的詳細資訊，請參閱 [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-logistic-regression-models.md)。  
  
###  <a name="bkmk_Query4"></a> 範例查詢 4:針對離散值進行預測  
 羅吉斯迴歸通常用於您要分析提供二進位結果之因數的案例中。 雖然教學課程中所使用的模型會預測連續值 **ServiceGrade**，不過在實際案例中，您可能會想要設定模型來預測服務等級是否符合某個離散化目標值。 或者，您可能會先使用連續值來輸出預測，然後再將預測的結果分組成 **良好**、 **普通**或 **差**。  
  
 下列範例說明如何變更可預測屬性的分組方式。 若要這樣做，您可以建立採礦結構的複本，然後變更目標資料行的離散化方法，讓這些值成為分組值而非連續值。  
  
 下列程序描述如何變更撥接中心資料內 Service Grade 值的分組方式。  
  
##### <a name="to-create-a-discretized-version-of-the-call-center-mining-structure-and-models"></a>建立離散化版本的客服中心採礦結構和模型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的方案總管中，展開 [採礦結構]。  
  
2.  以滑鼠右鍵按一下 Call Center.dmm，然後選取 [複製]。  
  
3.  以滑鼠右鍵按一下 [採礦結構] 並選取 [貼上]。 如此就會加入名為「話務中心 1」的新採礦結構。  
  
4.  以滑鼠右鍵按一下新的採礦結構並選取 [重新命名]。 輸入新的名稱：**話務中心離散化**。  
  
5.  按兩下新採礦結構，以在設計師中開啟。 請注意，所有的採礦模型都已進行複製，而且都具有延伸模組 1。 請暫時保留這些名稱。  
  
6.  在 [採礦結構] 索引標籤中，以滑鼠右鍵按一下 Service Grade 的資料行，然後選取 [屬性]。  
  
7.  變更`Content`屬性從**連續**要**Discretized**。 變更`DiscretizationMethod`屬性，以**叢集**。 針對 DiscretizationBucketCount 輸入 **3**。  
  
    > [!NOTE]  
    >  這些參數只用來說明此程序，並不一定會產生有效的模型。  
  
8.  在 [採礦模型] 功能表中，選取 [處理採礦結構和所有模型]。  
  
 下列範例查詢是以這個離散化模型為基礎，並且預測一週內指定之日期的服務等級，以及每個預測結果的機率。  
  
```  
SELECT  
  (PredictHistogram([Call Center_LR 1].[Service Grade])) as [Predictions]  
FROM  
  [Call Center_LR 1]  
NATURAL PREDICTION JOIN  
(SELECT 'Saturday' AS [Day Of Week]) AS t    
```  
  
 預期的結果：  
  
 **預測**  
  
|服務等級|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|-------------------|--------------|------------------|--------------------------|---------------|------------|  
|0.10872718383125|35.7246504770641|0.425293458060287|0.0170168360030293|0|0|  
|0.05855769230625|31.7098880800703|0.377498667619885|0.020882020060454|0|0|  
|0.170169491525|15.6109159883202|0.185844237956192|0.0661386571386049|0|0|  
||0.954545454545455|0.0113636363636364|0.0113636363636364|0|0|  
  
 請注意，預測的結果已經依照指定的方式分組成三個類別。不過，這些分組是以資料中實際值的群集為基礎，而非您可能設定為商務目標的二進位值。  
  
## <a name="list-of-prediction-functions"></a>預測函數的清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 羅吉斯迴歸演算法支援下表所列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用量|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|確定某個節點是否為模型中另一個節點的子系。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|傳回指定狀態的已調整機率。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|傳回指定之資料行的一個或一組預測值。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|傳回指定狀態的機率。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|傳回預測值的標準差。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|傳回指定狀態的支援值。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|傳回指定之資料行的變異數。|  
  
 如需所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法通用函數的清單，請參閱[一般預測函數 &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)。 如需特定函數的語法，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
> [!NOTE]  
>  若是類神經網路與羅吉斯迴歸模型，[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx) 函數會傳回代表整個模型之定型集大小的單一值。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢](data-mining-queries.md)   
 [Microsoft 羅吉斯迴歸演算法](microsoft-logistic-regression-algorithm.md)   
 [Microsoft 羅吉斯迴歸演算法技術參考](microsoft-logistic-regression-algorithm-technical-reference.md)   
 [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-logistic-regression-models.md)   
 [第 5 課：建立類神經網路和羅吉斯迴歸模型&#40;中繼資料採礦教學課程&#41;](../../tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)  
  
  
