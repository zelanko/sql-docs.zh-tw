---
title: 時間序列模型查詢範例 |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fb280c856b6e7231c078bf830be4a10f9ecc4723
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="time-series-model-query-examples"></a>時間序列模型查詢範例
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您針對資料採礦模型建立查詢時，可以建立內容查詢來提供有關分析期間所發現之模式的詳細資料，或是建立預測查詢來使用模型中的模式，為新的資料進行預測。 例如，時間序列模型的內容查詢可能會提供有關所偵測到之週期性結構的其他詳細資料，而預測查詢則為您提供下 5-10 個時間配量的預測。 您也可以使用查詢來擷取有關模型的中繼資料。  
  
 本章節將說明如何針對以 Microsoft 時間序列演算法為根據的模型來建立兩種查詢。  
  
 **內容查詢**  
  
 [擷取模型的週期性提示](#bkmk_Query1)  
  
 [擷取 ARIMA 模型的方程式](#bkmk_Query2)  
  
 [擷取 ARTxp 模型的方程式](#bkmk_Query3)  
  
 **預測查詢**  
  
 [了解取代和擴充時間序列資料的時機](#bkmk_ReplaceExtend)  
  
 [使用 EXTEND_MODEL_CASES 做出預測](#bkmk_EXTEND)  
  
 [使用 REPLACE_MODEL_CASES 做出預測](#bkmk_REPLACE)  
  
 [時間序列模型中的遺漏值替代](#bkmk_MissingValues)  
  
## <a name="getting-information-about-a-time-series-model"></a>取得有關時間序列模型的資訊  
 模型內容查詢可以提供有關此模型的基本資訊，例如在建立模型時所使用的參數以及上次處理模型的時間。 下列範例說明使用資料採礦結構描述資料列集來查詢模型內容的基本語法。  
  
###  <a name="bkmk_Query1"></a> 範例查詢 1：擷取模型的週期性提示  
 您可以擷取時間序列中所找到的週期性，其方式是查詢 ARIMA 樹狀結構或 ARTXP 樹狀結構。 但是，完成之模型中的週期性可能不會與當您建立模型時指定為提示的週期相同。 若要擷取當您建立模型時提供為參數的提示，您可以使用下列 DMX 陳述式來查詢採礦模型內容結構描述資料列集：  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = '<model name>'  
```  
  
 部分結果：  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY = 0.1，MINIMUM_SUPPORT = 10，PERIODICITY_HINT ={1,3}，...|  
  
 預設週期性提示為 {1}，而且會出現在所有模型中；這個範例模型是使用其他提示所建立，這個提示可能不會出現在最終模型中。  
  
> [!NOTE]  
>  這裡的結果已被截斷來提高可讀性。  
  
  
###  <a name="bkmk_Query2"></a> 範例查詢 2：擷取 ARIMA 模型的方程式  
 您可以查詢個別樹狀結構中的任何節點來擷取 ARIMA 模型的方程式。 請記住，ARIMA 模型中的每一個樹狀結構都代表不同的週期性，而且如果有多個資料數列，每一個資料數列都將有它自己的一組週期性樹狀結構。 因此，若要擷取特定資料數列的方程式，您必須先識別此樹狀結構。  
  
 例如，TA 前置詞告訴您此節點是 ARIMA 樹狀結構的一部分，而 TS 前置詞則用於 ARTXP 樹狀結構。 您可以尋找所有的 ARIMA 根樹狀結構，其方式是查詢具有 NODE_TYPE 值 27 之節點的模型內容。 您也可以使用 ATTRIBUTE_NAME 的值來尋找特定資料數列的 ARIMA 根節點。 此查詢範例會尋找代表在歐洲地區銷售之 R250 型號數量的 ARIMA 節點。  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM Forecasting.CONTENT  
WHERE ATTRIBUTE_NAME = 'R250 Europe: Quantity"  
AND NODE_TYPE = 27  
```  
  
 使用這個節點識別碼可以擷取有關此樹狀結構之 ARIMA 方程式的詳細資料。 下列 DMX 陳述式會擷取資料數列的簡短形式 ARIMA 方程式。 此外，也會從巢狀資料表 NODE_DISTRIBUTION 擷取截距。 在此範例中，此方程式是藉由參考節點唯一識別碼 TA00000007 來取得。 但是，您可能必須使用不同的節點識別碼，而且可能會取得與模型稍微不同的結果。  
  
```  
SELECT FLATTENED NODE_CAPTION as [Short equation],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE   
FROM NODE_DISTRIBUTION) as t  
FROM Forecasting.CONTENT  
WHERE NODE_NAME = 'TA00000007'  
```  
  
 範例結果：  
  
|簡短的方程式|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|--------------------|-----------------------|------------------------|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Intercept)|15.24….|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|1|  
|ARIMA (2,0,7)x(1,0,2)(12)|R250 Europe:Quantity(Periodicity)|12|  
  
 如需如何解譯這項資訊的詳細資訊，請參閱[時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
  
###  <a name="bkmk_Query3"></a> 範例查詢 3：擷取 ARTXP 模型的方程式  
 如果是 ARTxp 模型，每一層的樹狀結構上會儲存不同的資訊。 如需 ARTxp 模型的結構及如何解譯方程式內資訊的詳細資訊，請參閱[時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
 下列 DMX 陳述式會擷取屬於 ARTxp 樹狀結構之一部分的資訊，該資訊代表在歐洲銷售之 R250 型號的數量。  
  
> [!NOTE]  
>  巢狀資料表資料行 VARIANCE 的名稱必須括在括號內，以便與同名的保留關鍵字區別。 巢狀資料表資料行 PROBABILITY 和 SUPPORT 並未包括在其中，因為在大多數情況下，這兩者是空白的。  
  
```  
SELECT NODE_CAPTION as [Split information],   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
   [VARIANCE]  
   FROM NODE_DISTRIBUTION) AS t  
FROM Forecasting.CONTENT  
WHERE NODE_ATTRIBUTE_NAME = 'R250 Europe:Quantity'  
AND NODE_TYPE = 15  
```  
  
 如需如何解譯這項資訊的詳細資訊，請參閱[時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
  
## <a name="creating-predictions-on-a-time-series-model"></a>建立時間序列模型的預測  
 從 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]開始，您就可以將新的資料加入至時間序列模型，並自動將新的資料併入模型中。 您可以使用下列兩種方式的其中一種，將新的資料加入至時間序列採礦模型：  
  
-   使用 **PREDICTION JOIN** 將外部來源中的資料聯結至定型資料。  
  
-   使用單一預測查詢，一次為資料提供一個配量。 如需如何建立單一預測查詢的資訊，請參閱 [資料採礦查詢工具](../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
###  <a name="bkmk_ReplaceExtend"></a> 了解取代和擴充作業的行為  
 當您將新的資料加入時間序列模型時，可以指定是要擴充還是取代定型資料：  
  
-   **擴充：** 當您擴充資料數列時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會在現有定型資料的結尾加入新的資料。 定型案例的數目也會增加。  
  
     擴充此模型案例對於持續以新的資料更新模型非常實用。 例如，如果您想要讓定型集隨著時間成長，只要擴充模型即可。  
  
     若要擴充資料，您會在時間序列模型上建立 **PREDICTION JOIN** 、指定新資料的來源，並使用 **EXTEND_MODEL_CASES** 引數。  
  
-   **取代：** 當您取代資料數列中的資料時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會保留定型的模型，但是會使用新的資料來取代部分或所有現有的定型案例。 因此，定型資料的大小絕對不會改變，但是案例本身則會持續被更新的資料所取代。 如果您提供足夠的新資料，您可以使用完全新的序列來取代定型資料。  
  
     當您想要定型一組案例上的模型，然後將該模型套用到不同的資料數列時，取代模型案例會非常實用。  
  
     若要取代資料，您會在時間序列模型上建立 **PREDICTION JOIN** 、指定新資料的來源，並使用 **REPLACE_MODEL_CASES** 引數。  
  
> [!NOTE]  
>  當您加入新的資料時，將無法做出歷程記錄預測。  
  
 不論您要擴充還是取代定型資料，預測一定會開始於原始定型集結束的時間戳記。 換句話說，如果您的新資料包含 n 個時間配量，而且您要求時間步驟 1 到 n 的預測，則預測將會符合新資料的相同期間，而不會取得新的預測。  
  
 若要取得未與新資料重疊之期間的新預測，您必須在時間配量 n+1 上開始預測，或是確定您有要求其他的時間配量。  
  
 例如，假設現有的模型有六個月的資料。 您想要加入最後三個月的銷售數字來擴充這個模型， 同時，您想要對未來三個月做出預測。 如果加入新的資料時只要取得新的預測，請將起點指定為時間配量 4，並將結束點指定為時間配量 7。 您一共可以要求六個預測，但是前三個預測的時間配量會與剛加入的新資料重疊。  
  
 如需查詢範例及使用 **REPLACE_MODEL_CASES** 和 **EXTEND_MODEL_CASES**之語法的詳細資訊，請參閱 [PredictTimeSeries &#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md)。  
  
  
###  <a name="bkmk_EXTEND"></a> 使用 EXTEND_MODEL_CASES 做出預測  
 預測行為會因為您要擴充還是取代模型案例而異。 當您擴充模型時，新的資料會附加到序列的結尾，而且定型集的大小會增加。 但是，用於預測查詢的時間配量一定會開始於原始序列的結尾。 因此，如果您加入三個新的資料點，並要求六個預測，則傳回的前三個預測會與新的資料重疊。 在此情況下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會傳回實際的新資料點，而不是做出預測，直到所有新的資料點都用完為止。 然後， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會根據複合系列來做出預測。  
  
 這個行為可讓您加入新的資料，然後在預測圖中顯示實際的銷售數字，而不是查看投影。  
  
 例如，若要加入三個新資料點，並做出三個新的預測，您會執行以下作業：  
  
-   在時間序列模型上建立 **PREDICTION JOIN** ，並指定這三個月新資料的來源。  
  
-   要求六個時間配量的預測。 若要這樣做，請指定 6 個時間配量，其中起點是時間配量 1，而結束點則是時間配量 7。 這個情況只適用於 EXTEND_MODEL_CASES。  
  
-   如果只要取得新的預測，請將起點指定為時間配量 4，並將結束點指定為時間配量 7。  
  
-   您必須使用 **EXTEND_MODEL_CASES**引數。  
  
     這樣會傳回前三個時間配量的實際銷售數字，並針對接下來三個時間配量傳回根據此擴充模型的預測。  
  
  
###  <a name="bkmk_REPLACE"></a> 使用 REPLACE_MODEL_CASES 做出預測  
 當您取代模型中的案例時，此模型的大小會維持相同，但是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會取代此模型中的個別案例。 在交叉預測以及將訓練資料集維持一致大小非常重要的案例下，這種作法會很有用。  
  
 例如，假設其中一個存放區的銷售資料不足。 您可以建立一般模型，其方式是將特定區域中所有存放區的銷售量加以平均，然後定型模型。 然後，若要在沒有足夠銷售資料的情況下為存放區做出預測，您可以只針對該存放區的新銷售資料建立 **PREDICTION JOIN** 。 當您這樣做時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會保留衍生自區域模型的模式，但是會使用個別存放區中的資料來取代現有的定型案例。 因此，您的預測值將會比較接近於個別存放區的趨勢線。  
  
 當您使用 **REPLACE_MODEL_CASES** 引數時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會持續將新的案例加入案例集的結尾，並從此案例集的開頭刪除對應的數目。 如果您加入的資料多於原始定型集中的資料， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會捨棄最早的資料。 如果您提供足夠的新值，可以根據完全新的資料來做出預測。  
  
 例如，假設您在包含 1000 個資料列的案例資料集上定型您的模型， 然後您加入 100 列的新資料。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會從定型集中卸除前 100 個資料列，並將 100 列的新資料加入一共 1000 個資料列的集合結尾。 如果您加入 1100 列的新資料，只會使用最近的 1000 個資料列。  
  
 以下是另一個範例。 若要加入三個新月份的資料，並做出三個新的預測，您會執行以下動作：  
  
-   在時間序列模型上建立 **PREDICTION JOIN** ，並使用 **REPLACE_MODEL_CASE** 引數。  
  
-   指定三個月新資料的來源。 這些資料可能與原始定型資料的來源完全不同。  
  
-   要求六個時間配量的預測。 若要這樣做，請指定 6 個時間配量，或是將起點指定為時間配量 1，而將結束點指定為時間配量 7。  
  
    > [!NOTE]  
    >  與 **EXTEND_MODEL_CASES**不同的是，您無法傳回與加入的輸入資料相同的值。 傳回的所有六個值都是根據更新模型所做的預測，其中包含舊的和新的資料。  
  
    > [!NOTE]  
    >  從 REPLACE_MODEL_CASES 的時間戳記 1 開始，您會根據新的資料取得新的預測，新的資料會取代舊的訓練資料。  
  
 如需查詢範例及使用 **REPLACE_MODEL_CASES** 和 **EXTEND_MODEL_CASES**之語法的詳細資訊，請參閱 [PredictTimeSeries &#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md)。  
  
  
###  <a name="bkmk_MissingValues"></a> 時間序列模型中的遺漏值替代  
 當您使用 **PREDICTION JOIN** 陳述式將新的資料加入時間序列模型中時，新的資料集不能有任何遺漏值。 如果有任何數列不完整，此模型必須提供遺漏的值，其方式是使用 null、數值平均、特定的數值平均或預測值。 如果您指定 **EXTEND_MODEL_CASES**， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用根據原始模型的預測來取代遺漏值。 如果您使用 **REPLACE_MODEL_CASES**， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用您在 *MISSING_VALUE_SUBSTITUTION* 參數中指定的值來取代遺漏值。  
  
## <a name="list-of-prediction-functions"></a>預測函數的清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法支援下表所列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用方式|  
|[Lag & #40; DMX & #41;](../../dmx/lag-dmx.md)|傳回目前案例的日期與定型集的最後日期之間的時間配量數目。<br /><br /> 這個函數的典型用法就是用來識別最近的定型案例，好讓您可以擷取有關案例的詳細資料。|  
|[PredictNodeId & #40; DMX & #41;](../../dmx/predictnodeid-dmx.md)|傳回指定之可預測資料行的節點識別碼。<br /><br /> 這個函數的典型用法就是用來識別產生特定預測值的節點，好讓您可以檢閱與此節點有關的案例，或擷取方程式和其他詳細資料。|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|傳回指定之可預測資料行中預測的標準差。<br /><br /> 此函數會取代 INCLUDE_STATISTICS 引數，時間序列模型不支援這個引數。|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|傳回指定之可預測資料行中預測的變異數。<br /><br /> 此函數會取代 INCLUDE_STATISTICS 引數，時間序列模型不支援這個引數。|  
|[PredictTimeSeries & #40; DMX & #41;](../../dmx/predicttimeseries-dmx.md)|傳回時間序列的預測記錄值或未來預測值。<br /><br /> 您也可以使用一般預測函數 [Predict &#40;DMX&#41;](../../dmx/predict-dmx.md) 來查詢時間序列模型。|  
  
 如需所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法通用函數的清單，請參閱[一般預測函數 &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md)。 如需特定函數的語法，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](../../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 時間序列演算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft 時間序列演算法技術參考](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [時間序列模型 & #40; 的採礦模型內容Analysis Services-資料採礦 & #41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
