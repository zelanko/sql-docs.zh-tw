---
title: 第4課：使用 DMX 建立時間序列預測 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6b883e43-209d-489a-8dc3-9349f88acae8
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 772e5f5f71ca82dd18fec48730522c80e907414f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63312085"
---
# <a name="lesson-4-creating-time-series-predictions-using-dmx"></a>第 4 課：使用 DMX 建立時間序列預測
  在這堂課和下列課程中，您將使用資料採礦延伸模組（DMX），根據您在[第1課：建立時間序列的「採礦模型」和「採礦結構](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)」和[第2課：將採礦模型加入至時間序列採礦結構](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)中所建立的時間序列模型，來建立不同類型的預測。  
  
 有了時間序列模型，您有許多選擇可用來進行預測：  
  
-   在採礦模型中使用現有的模式和資料。  
  
-   在採礦模型中使用現有的模式，但是提供新的資料。  
  
-   將新的資料加入到模型中，或是更新模型。  
  
 這些預測類型的語法摘要列在底下：  
  
 預設時間序列預測  
 使用[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx) ，以從定型的採礦模型傳回指定的預測數目。  
  
 例如，請參閱[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)或[時間序列模型查詢範例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)。  
  
 EXTEND_MODEL_CASES  
 使用[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)搭配 EXTEND_MODEL_CASES 引數來加入新資料、擴充數列，並根據更新的採礦模型建立預測。  
  
 本教學課程包含的範例將示範如何使用 EXTEND_MODEL_CASES。  
  
 REPLACE_MODEL_CASES  
 使用[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)搭配 REPLACE_MODEL_CASES 引數，以新的資料數列取代原始資料，然後根據將採礦模型中的模式套用至新的資料數列來建立預測。  
  
 如需如何使用 REPLACE_MODEL_CASES 的範例，請參閱[第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   根據現有的資料建立查詢來取得預設的預測。  
  
 在下一課中，您將會執行下列相關工作：  
  
-   建立查詢來提供新的資料，並取得更新的預測。  
  
 除了使用 DMX 手動建立查詢以外，您也可以在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用預測查詢產生器來建立預測。  
  
## <a name="simple-time-series-prediction-query"></a>簡單時間序列預測查詢  
 第一個步驟是搭配 `SELECT FROM` 函數一起使用 `PredictTimeSeries` 陳述式來建立時間序列預測。 時間序列模型支援用來建立預測的簡化語法：您不需要提供任何輸入，只需要指定所要建立的預測數。 以下是您將使用之陳述式的一般範例：  
  
```  
SELECT <select list>   
FROM [<mining model name>]   
WHERE [<criteria>]  
```  
  
 選取清單可以包含模型中的資料行，例如您要為其建立預測的產品線名稱，或是預測函數（例如， [&#40;dmx&#41;](/sql/dmx/lag-dmx)或[PredictTimeSeries &#40;Dmx&#41;](/sql/dmx/predicttimeseries-dmx)的 Lag，特別是針對時間序列的採礦模型。  
  
#### <a name="to-create-a-simple-time-series-prediction-query"></a>若要建立簡單的時間序列預測查詢  
  
1.  在**物件總管**中，以滑鼠右鍵按一下的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例，指向 [追加**查詢**]，然後按一下 [ **DMX**]。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將此陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <select list>   
    ```  
  
     成為：  
  
    ```  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    ```  
  
     第一行會從可識別此數列的採礦模型中擷取值。  
  
     第二行和第三行會使用 `PredictTimeSeries` 函數。 每一行都會預測不同的屬性 (`[Quantity]` 或 `[Amount]`)。 可預測屬性名稱後面的數字會指定所要預測的時間步驟數。  
  
     `AS` 子句是用來針對每一個預測函數傳回的資料行提供一個名稱。 如果您不提供別名，則當傳回這兩個資料行時，預設都會將其加上 `Expression` 標籤。  
  
4.  取代下列項目：  
  
    ```  
    [<mining model>]   
    ```  
  
     成為：  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
5.  取代下列項目：  
  
    ```  
    WHERE [criteria>]   
    ```  
  
     成為：  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT  
    [Forecasting_MIXED].[ModelRegion],  
    PredictTimeSeries([Forecasting_MIXED].[Quantity],6) AS PredictQty,  
    PredictTimeSeries ([Forecasting_MIXED].[Amount],6) AS PredictAmt  
    FROM   
    [Forecasting_MIXED]  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
6.  **在 [檔案**] 功能表上，按一下 [**將 DMXQuery1 另存為**]。  
  
7.  在 [**另存**新檔] 對話方塊中，流覽至適當的資料夾，並`SimpleTimeSeriesPrediction.dmx`將檔案命名為。  
  
8.  在工具列上，按一下 [**執行**] 按鈕。  
  
     此查詢會針對 `WHERE` 子句中指定之產品和區域的兩個組合，每個組合各傳回 6 個預測。  
  
 在下一課中，您將會建立查詢來提供新資料給模型，然後將該項預測的結果與您剛才建立的預測做比較。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [第 5 課：擴充時間序列模型](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [DMX&#41;的 PredictTimeSeries &#40;](/sql/dmx/predicttimeseries-dmx)   
 [DMX&#41;的 Lag &#40;](/sql/dmx/lag-dmx)   
 [時間序列模型查詢範例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
  
