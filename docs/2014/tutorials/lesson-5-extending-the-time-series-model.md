---
title: 第5課：擴充時間序列模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7aad4946-c903-4e25-88b9-b087c20cb67d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2716e985897f8115d189d9410b7cdb13fb1af291
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62822060"
---
# <a name="lesson-5-extending-the-time-series-model"></a>第 5 課：擴充時間序列模型
  在 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise 中，您可以將新的資料加入至時間序列模型，並自動將新的資料併入此模型中。 您可以使用下列兩種方式的其中一種，將新的資料加入至時間序列採礦模型：  
  
-   使用 PREDICTION JOIN 將外部來源中的資料聯結至定型資料。  
  
-   使用單一預測查詢，一次為資料提供一個配量。  
  
 例如，假設您在幾個月以前已經針對現有的銷售資料定型採礦模型。 當您取得新的銷售時，您可能會想要更新銷售預測來併入新的資料。 您可以在一個步驟中完成這項處理，其方式是提供新的銷售數字當做輸入資料，然後根據複合資料集來產生新的預測。  
  
## <a name="making-predictions-with-extend_model_cases"></a>使用 EXTEND_MODEL_CASES 做出預測  
 下列是使用 EXTEND_MODEL_CASES 之時間序列預測的一般範例。 第一個範例可讓您從原始模型的最後一個時間步驟開始指定預測數目：  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>]  
```  
  
 第二個範例可讓您指定預測應該開始及應該結束的時間步驟。 當您要擴充模型案例時，這個選項非常重要，因為根據預設，用於預測查詢的時間步驟一定會從原始數列的結尾開始。  
  
```  
SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n-start, n-end, EXTEND_MODEL_CASES)   
FROM <mining model>  
PREDICTION JOIN <source query>  
[WHERE <criteria>}  
```  
  
 在本教學課程中，您將會建立這兩種查詢。  
  
#### <a name="to-create-a-singleton-prediction-query-on-a-time-series-model"></a>若要針對時間序列模型建立單一預測查詢  
  
1.  在**物件總管**中，以滑鼠右鍵按一下的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例，指向 [追加**查詢**]，然後按一下 [ **DMX**]。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將單一陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    SELECT [<model columns>,] PredictTimeSeries(<table column reference>, n, EXTEND_MODEL_CASES)   
    ```  
  
     成為：  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    ```  
  
     第一行會從可識別此數列的模型中擷取值。  
  
     第二行包含預測函數，該函數會取得 Quantity 的六項預測。 別名 `PredictQty` 會指派給預測結果資料行，讓您更輕鬆地了解結果。  
  
4.  取代下列項目：  
  
    ```  
    FROM <mining model>  
    ```  
  
     成為：  
  
    ```  
    FROM [Forecasting_MIXED]  
    ```  
  
5.  取代下列項目：  
  
    ```  
    PREDICTION JOIN <source query>  
    ```  
  
     成為：  
  
    ```  
    NATURAL PREDICTION JOIN   
    (  
       SELECT 1 AS [Reporting Date],  
       '10' AS [Quantity],  
       'M200 Europe' AS [Model Region]  
       UNION SELECT  
       2 AS [Reporting Date],  
       15 AS [Quantity]),  
       'M200 Europe' AS [Model Region]  
    ) AS t  
    ```  
  
6.  取代下列項目：  
  
    ```  
    [WHERE <criteria>]  
    ```  
  
     成為：  
  
    ```  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    SELECT [Model Region],  
    PredictTimeSeries([Quantity],6, EXTEND_MODEL_CASES) AS PredictQty  
    FROM  
       [Forecasting_MIXED]  
    NATURAL PREDICTION JOIN   
       SELECT 1 AS [ReportingDate],  
      '10' AS [Quantity],  
      'M200 Europe' AS [ModelRegion]  
    UNION SELECT  
      2 AS [ReportingDate],  
      15 AS [Quantity]),  
      'M200 Europe' AS [ModelRegion]  
    ) AS t  
    WHERE [ModelRegion] = 'M200 Europe' OR  
    [ModelRegion] = 'M200 Pacific'  
    ```  
  
7.  **在 [檔案**] 功能表上，按一下 [**將 DMXQuery1 另存為**]。  
  
8.  在 [**另存**新檔] 對話方塊中，流覽至適當的資料夾，並`Singleton_TimeSeries_Query.dmx`將檔案命名為。  
  
9. 在工具列上，按一下 [**執行**] 按鈕。  
  
     此查詢會傳回 M200 自行車在歐洲和太平洋地區銷售數量的預測。  
  
## <a name="understanding-prediction-start-with-extend_model_cases"></a>從 EXTEND_MODEL_CASES 開始了解預測  
 現在您已經根據原始模型建立預測，而且有了新的資料之後，您就可以比較結果來查看更新銷售資料會如何影響預測。 在您這樣做之前，請先檢閱您剛才建立的程式碼，並注意以下事項：  
  
-   您只為歐洲地區提供新的資料。  
  
-   您只提供兩個月的新資料。  
  
 下表顯示為 M200 Europe 所提供的新值要如何影響預測。 您並未提供 M200 產品在太平洋地區的任何新資料，但是會呈現這個數列進行比較：  
  
 **產品和地區： M200 歐洲**  
  
|||||  
|-|-|-|-|  
|||現有的模型 (`PredictTimeSeries`)|具有更新銷售資料的模型 (具有 `PredictTimeSeries` 的 `EXTEND_MODEL_CASES`)|  
|M200 Europe|上午 7/25/2008 12:00:00|77|10|  
|M200 Europe|上午 8/25/2008 12:00:00|64|15|  
|M200 Europe|上午 9/25/2008 12:00:00|59|72|  
|M200 Europe|上午 10/25/2008 12:00:00|56|69|  
|M200 Europe|上午 11/25/2008 12:00:00|56|68|  
|M200 Europe|12/25/2008 12:00:00 AM|74|89|  
  
 **產品和地區： M200 太平洋**  
  
|||||  
|-|-|-|-|  
|||現有的模型 (`PredictTimeSeries`)|具有更新銷售資料的模型 (具有 `PredictTimeSeries` 的 `EXTEND_MODEL_CASES`)|  
|M200 Pacific|上午 7/25/2008 12:00:00|41|41|  
|M200 Pacific|上午 8/25/2008 12:00:00|44|44|  
|M200 Pacific|上午 9/25/2008 12:00:00|38|38|  
|M200 Pacific|上午 10/25/2008 12:00:00|41|41|  
|M200 Pacific|上午 11/25/2008 12:00:00|36|36|  
|M200 Pacific|12/25/2008 12:00:00 AM|39|39|  
  
 您可以從這些結果看到兩件事：  
  
-   M200 Europe 數列的前兩個預測與您所提供的新資料完全相同。 根據設計，Analysis Services 會傳回實際的新資料點，而不是做出預測。 這是因為當您要擴充模型案例時，用於預測查詢的時間步驟一定會從原始數列的結尾開始。 因此，如果您加入兩個新的資料點，則傳回的前兩個預測將會與新的資料重疊。  
  
-   當所有新的資料點都使用完之後，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會根據更新的模型做預測。 因此從 2005 年九月開始，您可以看到左欄中原始模型的 M200 Europe 與右欄中使用 EXTEND_MODEL_CASES 的模型之間的預測差異。 這兩個預測不同是因為已經使用新的資料來更新此模型。  
  
## <a name="using-start-and-end-time-steps-to-control-predictions"></a>使用開始和結束時間步驟來控制預測  
 當您擴充模型時，新的資料一定會附加到數列的結尾。 但是，基於預測的目的，用於預測查詢的時間配量會開始於原始數列的結尾。 如果您在加入新的資料時只要取得新的預測，則必須將起點指定為時間配量的數目。 例如，如果您要加入兩個新的資料點，而且想要做出四個新預測，您應該會這樣做：  
  
-   在時間序列模型上建立 PREDICTION JOIN，並指定兩個月的新資料。  
  
-   要求四個時間配量的預測，其中的起點是 3，而結束點則是時間配量 6。  
  
 換句話說，如果您的新資料包含 n 個時間配量，而且您要求時間步驟1到 n 的預測，則預測將會與新資料的相同期間一致。 若要取得資料未涵蓋之期間的新預測，您必須在新資料序列之後的時間配量 n+1 上開始預測，或是確定您有要求其他的時間配量。  
  
> [!NOTE]  
>  當您加入新的資料時，將無法做出歷程記錄預測。  
  
 下列範例示範 DMX 陳述式，該陳述式可讓您針對上一個範例中的兩個數列僅取得新的預測。  
  
```  
SELECT [Model Region],  
PredictTimeSeries([Quantity],3,6, EXTEND_MODEL_CASES) AS PredictQty  
FROM  
   [Forecasting_MIXED]  
NATURAL PREDICTION JOIN   
   SELECT 1 AS [ReportingDate],  
  '10' AS [Quantity],  
  'M200 Europe' AS [ModelRegion]  
UNION SELECT  
  2 AS [ReportingDate],  
  15 AS [Quantity]),  
  'M200 Europe' AS [ModelRegion]  
) AS t  
WHERE [ModelRegion] = 'M200 Europe'  
```  
  
 預測結果從時間配量 3 開始，這是在您提供兩個月的新資料之後。  
  
 **產品和地區： M200 歐洲**  
  
 具有更新資料的模型 (具有 EXTEND_MODEL_CASES 的 PredictTimeSeries)  
  
||||  
|-|-|-|  
|M200 Europe|上午 9/25/2008 12:00:00|72|  
|M200 Europe|上午 10/25/2008 12:00:00|69|  
|M200 Europe|上午 11/25/2008 12:00:00|68|  
|M200 Europe|12/25/2008 12:00:00 AM|89|  
  
## <a name="making-predictions-with-replace_model_cases"></a>使用 REPLACE_MODEL_CASES 做出預測  
 當您想要定型一組案例上的模型，然後將該模型套用到不同的資料數列時，取代模型案例會非常實用。 本案例的詳細逐步解說會在[第2課：建立預測案例中顯示 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。  
  
## <a name="see-also"></a>另請參閱  
 [時間序列模型查詢範例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)  
  
  
