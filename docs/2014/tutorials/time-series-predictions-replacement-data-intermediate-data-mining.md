---
title: 時間序列預測使用取代資料 （中繼資料採礦教學課程） |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a23a6e1d-1d49-41ea-8314-925dc8e4df5e
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d5639aa63affadcdf79acc6029840e7025081245
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312466"
---
# <a name="time-series-predictions-using-replacement-data-intermediate-data-mining-tutorial"></a>使用取代資料執行時間序列預測 (中繼資料採礦教學課程)
  在這項工作中，您將會根據全球銷售資料建立新的模型。 接著，您將會建立預測查詢，此查詢會將全球銷售模型套用到其中一個個別地區。  
  
## <a name="building-a-general-model"></a>建立一般模型  
 請記得原始採礦模型結果的分析揭露地區之間和產品線之間有很大的差異。 例如，北美洲對於 M200 模型的銷售非常強，而 T1000 模型的銷售則沒有這麼強。 不過，分析之所以複雜，是因為有些數列沒有很多資料，或者資料是在不同的時間點開始。 此外還缺少某些資料。  
  
 ![序列預測 M200 與 T1000 數量](../../2014/tutorials/media/6series-defaultforecasting.gif "序列預測 M200 與 T1000 數量")  
  
 為了解決部分資料品質問題，您決定合併全球銷售資料，並使用該組一般銷售趨勢，建立可用來預測任何地區未來銷售的模型。  
  
 當您建立預測時，將會使用定型全球銷售資料時所產生的模式，但會以各地區的銷售資料來取代歷程記錄資料點。 這樣會保留趨勢的形狀，但預測的值會與各地區和模型的歷程銷售數字相吻合。  
  
## <a name="performing-cross-prediction-with-a-time-series-model"></a>在時間序列模型上執行交叉預測  
 使用某個數列的資料來預測另一個數列中的趨勢，這個程序稱為交叉預測。 您可以在許多案例中使用交叉預測：例如，您可能決定電視銷售是整體經濟活動的絕佳預測指標，而將經過電視銷售定型的模型套用至一般經濟資料。  
  
 在 SQL Server 資料採礦，您必須執行交叉預測使用 REPLACE_MODEL_CASES 參數的函式的引數內[PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)。  
  
 在下一個工作中，您將會了解如何使用 REPLACE_MODEL_CASES。 您將使用合併的全球銷售資料來建立模型，然後建立預測查詢，將一般模型對應至取代資料。  
  
 此工作中假設您現在已經熟悉如何建立資料採礦模型，因此簡化了建立模型的指示。  
  
#### <a name="to-build-a-mining-structure-and-mining-model-using-the-aggregated-data"></a>若要使用彙總資料建立採礦結構和採礦模型  
  
1.  在**方案總管 中**，以滑鼠右鍵按一下**採礦結構**，然後選取**新的採礦結構**即可啟動資料採礦精靈。  
  
2.  在資料採礦精靈中，進行下列選擇：  
  
    -   演算法：Microsoft 時間序列  
  
    -   將您稍早在此進階課程中建立的資料來源當做模型的來源使用。 請參閱[進階時間序列預測&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)。  
  
         資料來源檢視： `AllRegions`  
  
    -   針對數列索引鍵和時間索引鍵，選擇下列資料行：  
  
         時間索引鍵： ReportingDate  
  
         索引鍵： 區域  
  
    -   針對 `Input` 和 `Predict`，選擇下列資料行：  
  
         SumQty  
  
         SumAmt  
  
         AvgAmt  
  
         AvgQty  
  
    -   如**採礦結構名稱**，類型： `All Regions`  
  
    -   如**採礦模型名稱**，類型： `All Regions`  
  
3.  處理新結構和新模型。  
  
#### <a name="to-build-the-prediction-query-and-map-the-replacement-data"></a>若要建立預測查詢及對應取代資料  
  
1.  如果模型尚未開啟，按兩下 AllRegions 結構，並在資料採礦設計師中，按一下**採礦模型預測** 索引標籤。  
  
2.  在**採礦模型**窗格中，應該已選取 AllRegions 模型。 如果未選取，按一下**選取模型**，然後選取 AllRegions 模型。  
  
3.  在**選取輸入資料表**] 窗格中，按一下 [**選取案例資料表**。  
  
4.  在**選取資料表**對話方塊中，變更資料來源為 T1000 Pacific Region，，然後按一下**確定**。  
  
5.  以滑鼠右鍵按一下採礦模型和輸入的資料之間的聯結線，然後選取**修改連接**。 將資料來源檢視中的資料對應至模型，如下所示：  
  
    1.  確認採礦模型中的 ReportingDate 資料行對應至輸入資料中的 ReportingDate 資料行。  
  
    2.  在**修改對應**對話方塊中，模型資料行 AvgQty 的資料列中按一下 [下**資料表資料行**]，然後選取 [T1000 pacific.quantity]。 按一下 [確定] 。  
  
         這個步驟會將您在模型中建立用於預測平均數量的資料行對應到 T1000 數列中銷售數量的實際資料。  
  
    3.  無法對應在模型中的資料行區域至任何輸入資料行。  
  
         由於模型跨所有數列彙總資料，因此 T1000 Pacific 之類的數列值沒有相符項目，而且在執行預測查詢時，會引發錯誤。  
  
6.  現在，您將建立預測查詢。  
  
     首先，在結果中加入一個資料行，此資料行會從模型中輸出 AllRegions 標籤與預測。 如此一來，您就可以知道結果是以一般模型為基礎。  
  
    1.  在方格中，按一下第一個空白資料列，在**來源**，然後選取 AllRegions 採礦模型。  
  
    2.  如**欄位**，選取區域。  
  
    3.  如**別名**，型別**Model Used**。  
  
7.  接著在結果中加入另一個標籤，讓您得知預測是針對哪些數列。  
  
    1.  按一下空白的資料列，然後在**來源**，選取**自訂運算式**。  
  
    2.  在**別名**欄中，輸入**ModelRegion**。  
  
    3.  在**準則/引數**欄中，輸入`'T1000 Pacific'`。  
  
8.  現在，您將設定交叉預測函數。  
  
    1.  按一下空白的資料列，然後在**來源**，選取**預測函數**。  
  
    2.  在**欄位**欄中，選取**PredictTimeSeries**。  
  
    3.  如**別名**，型別**Predicted Values**。  
  
    4.  將 AvgQty 欄位從**採礦模型**窗格將**準則/引數**使用拖放作業的資料行。  
  
    5.  在**準則/引數**資料行中，於欄位名稱之後輸入下列文字： `,5, REPLACE_MODEL_CASES`  
  
         完整文字**準則/引數**文字方塊應，如下所示： `[AllRegions].[AvgQty],5,REPLACE_MODEL_CASES`  
  
9. 按一下**結果**。  
  
## <a name="creating-the-cross-prediction-query-in-dmx"></a>使用 DMX 建立交叉預測查詢  
 您可能注意到交叉預測有個問題：亦即，若要將一般模型套用至不同的資料數列，例如北美地區的 T1000 產品模型，您必須針對每個數列建立不同的查詢，才能將各組輸入對應至模型。  
  
 但是，您可以切換至 DMX 檢視並編輯建立的 DMX 陳述式，而不在設計工具中建立查詢。 例如，下列 DMX 陳述式代表您剛才建立的查詢：  
  
```  
SELECT  
      ([All Regions].[Region]) as [Model Used],  
      ('T-1000 Pacific') as [ModelRegion],  
      (PredictTimeSeries([All Regions].[Avg Qty],5, REPLACE_MODEL_CASES)) as [Predicted Quantity]  
     FROM [All Regions]  
PREDICTION JOIN  
    OPENQUERY([Adventure Works DW2003R2], 'SELECT [ReportingDate] FROM  
      (  
       SELECT  ReportingDate, ModelRegion, Quantity, Amount   
       FROM dbo.vTimeSeries   
       WHERE (ModelRegion = N''T1000 Pacific'')  
       ) as [T1000 Pacific]    ')   
    AS t  
ON   
[All Regions].[Reporting Date] = t.[ReportingDate]   
AND   
[All Regions].[Avg Qty] = t.[Quantity]  
```  
  
 若要將此套用到不同的模型，您只需編輯查詢陳述式來取代篩選條件並更新與每一個結果關聯的標籤。  
  
 例如，如果您以 'North America' 取代 'Pacific' 來變更篩選條件和資料行標籤，您將會得到 T1000 產品在北美的預測 (根據一般模型中的模式)。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [比較預測的預測模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [時間序列模型查詢範例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
