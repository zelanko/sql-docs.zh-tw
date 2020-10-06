---
description: PredictTimeSeries (DMX)
title: PredictTimeSeries (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 02b85cc4197b0ffafef7a83566e4041a7d290548
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727669"
---
# <a name="predicttimeseries-dmx"></a>PredictTimeSeries (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  傳回時間序列資料的預測未來值。 時間序列資料是連續的，而且可以儲存在巢狀資料表或案例資料表中。 **PredictTimeSeries**函式一律會傳回嵌套的資料表。  
  
## <a name="syntax"></a>語法  
  
```  
  
PredictTimeSeries(<table column reference>)  
PredictTimeSeries(<table column reference>, n)  
PredictTimeSeries(<table column reference>, n-start, n-end)  
PredictTimeSeries(<scalar column reference>)  
PredictTimeSeries(<scalar column reference>, n)  
PredictTimeSeries(<scalar column reference>, n-start, n-end)  
PredictTimeSeries(<table column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<table column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
PredictTimeSeries(<scalar column reference>, n-start, n-end, REPLACE_MODEL_CASES | EXTEND_MODEL_CASES) PREDICTION JOIN <source query>  
```  
  
## <a name="arguments"></a>引數  
 *\<table column reference>*, *\<scalar column referenc>*  
 指定要預測之資料行的名稱。 此資料行可以包含純量或表格式資料。  
  
 *n*  
 指定要預測之後續步驟的數目。 如果未指定 *n*的值，則預設值為1。  
  
 *n* 不可以是0。 如果您沒有至少進行一次預測，此函數會傳回錯誤。  
  
 *n-開始、n-1*  
 指定時間序列步驟的範圍。  
  
 *n-start* 必須是整數，而且不可以是0。  
  
 *n 端* 必須是大於 *n-start*的整數。  
  
 *\<source query>*  
 定義用於進行預測的外部資料。  
  
 REPLACE_MODEL_CASES | EXTEND_MODEL_CASES  
 指示如何處理新的資料。  
  
 REPLACE_MODEL_CASES 會指定應該使用新的資料來取代此模型中的資料點。 但是，預測是根據現有採礦模型中的模式。  
  
 EXTEND_MODEL_CASES 會指定新的資料應該加入到原始訓練資料集中。 未來只有在新的資料使用完畢以後，才會針對複合資料進行預測。  
  
 只有在使用 PREDICTION JOIN 陳述式加入新資料時，才可以使用這些引數。 如果您使用 PREDICTION JOIN 查詢而且未指定引數，預設值會是 EXTEND_MODEL_CASES。  
  
## <a name="return-type"></a>傳回類型  
 \<*table expression*>。  
  
## <a name="remarks"></a>備註  
 使用 PREDICTION JOIN 陳述式加入新資料時，[!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法不支援歷程記錄預測。  
  
 在 PREDICTION JOIN 中，預測程序永遠會在原始定型序列一結束之後的時間步驟開始。 即使您加入新資料也是如此。 因此， *n* 參數和 *n 開始* 參數值必須是大於0的整數。  
  
> [!NOTE]  
>  新資料的長度不會影響預測的起點。 因此，如果您要加入新資料，也想進行新預測，請確認有將預測的起始點設定為大於新資料長度的值，或按照新資料的長度擴充預測的結束點。  
  
## <a name="examples"></a>範例  
 下列範例顯示如何根據現有的時間序列模型進行預測：  
  
-   第一個範例顯示如何根據目前的模型進行指定之數目的預測。  
  
-   第二個範例示範如何使用 REPLACE_MODEL_CASES 參數，將指定之模型中的模式套用到新的資料集。  
  
-   第三個範例示範如何使用 EXTEND_MODEL_CASES 參數，以全新的資料更新採礦模型。  
  
 若要深入瞭解時間序列模型的使用方式，請參閱資料採礦教學 [課程，第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](/previous-versions/sql/sql-server-2016/ms169846(v=sql.130)) 和 [時間序列預測 DMX 教學](/previous-versions/sql/sql-server-2016/cc879270(v=sql.130))課程。  
  
> [!NOTE]  
>  您可能會從模型中取得不同的結果；提供底下範例的結果只是為了說明結果格式。  
  
### <a name="example-1-predicting-a-number-of-time-slices"></a>範例 1：預測時間配量數目  
 下列範例會使用 **PredictTimeSeries** 函數來傳回接下來三個時間步驟的預測，並將結果限制在歐洲和太平洋地區的 M200 系列。 在這個特定模型中，可預測屬性為 Quantity，所以您必須使用 `[Quantity]` 做為 PredictTimeSeries 函數的第一個引數。  
  
```  
SELECT FLATTENED  
    [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity],3)AS t   
FROM  
    [Forecasting]  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 Pacific'  
```  
  
 預期的結果：  
  
|Model Region|t.$TIME|t.Quantity|  
|------------------|-------------|----------------|  
|M200 Europe|上午 7/25/2008 12:00:00|121|  
|M200 Europe|上午 8/25/2008 12:00:00|142|  
|M200 Europe|上午 9/25/2008 12:00:00|152|  
|M200 Pacific|上午 7/25/2008 12:00:00|46|  
|M200 Pacific|上午 8/25/2008 12:00:00|44|  
|M200 Pacific|上午 9/25/2008 12:00:00|42|  
  
 在此範例中，FLATTENED 關鍵字用於讓結果更容易讀取。  如果您沒有使用 FLATTENED 關鍵字，而是傳回階層式資料列集，此查詢會傳回兩個資料行。 第一個資料行包含 [ModelRegion] 的值，而第二個資料行包含具有兩個資料行的巢狀資料表：用於顯示要預測之時間配量的 $TIME 以及包含預測值的 Quantity。  
  
### <a name="example-2-adding-new-data-and-using-replace_model_cases"></a>範例 2：加入新資料並使用 REPLACE_MODEL_CASES  
 假設您發現特定地區的資料不正確，而且您想要使用模型中的模式，但是要調整預測來符合新的資料。 或者，您可能會尋找具有更可靠之趨勢的另一個地區，而且想要將最可靠的模型套用到另一個地區的資料。  
  
 在這類情況下，您可以使用 REPLACE_MODEL_CASES 參數，並指定新的資料集當做歷程記錄資料使用。 這樣一來，將會根據指定之模型內的模式來做預測，但是將會從新資料點的結尾繼續順利進行。 如需此案例的完整逐步解說，請參閱 [&#40;元資料採礦教學課程&#41;的 Advanced Time Series 預測 ](/previous-versions/sql/sql-server-2016/cc879290(v=sql.130))。  
  
 下列 PREDICTION JOIN 查詢說明取代資料以及做出新預測的語法。 如果是取代資料，此範例會擷取 Amount 和 Quantity 資料行的值，並將每一個乘以二：  
  
```  
SELECT [Forecasting].[Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 3, REPLACE_MODEL_CASES)   
FROM  
    [Forecasting]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT [ModelRegion],   
    ([Quantity] * 2) as Quantity,  
    ([Amount] * 2) as Amount,  
      [ReportingDate]  
    FROM [dbo].vTimeSeries  
    WHERE ModelRegion = N''M200 Pacific''  
    ') AS t  
ON  
  [Forecasting].[Model Region] = t.[ Model Region] AND  
[Forecasting].[Reporting Date] = t.[ReportingDate] AND  
[Forecasting].[Quantity] = t.[Quantity] AND  
[Forecasting].[Amount] = t.[Amount]  
```  
  
 下表比較預測的結果。  
  
 原始預測：  
  
|Model Region|ReportingDate|數量|  
|-|-|-|  
|M200 Pacific|上午 7/25/2008 12:00:00|46|  
|M200 Pacific|上午 8/25/2008 12:00:00|44|  
|M200 Pacific|上午 9/25/2008 12:00:00|42|  
  
 更新的預測：  
  
|Model Region|ReportingDate|數量|  
|-|-|-|  
|M200 Pacific|上午 7/25/2008 12:00:00|91|  
|M200 Pacific|上午 8/25/2008 12:00:00|89|  
|M200 Pacific|上午 9/25/2008 12:00:00|84|  
  
### <a name="example-3-adding-new-data-and-using-extend_model_cases"></a>範例 3：加入新資料並使用 EXTEND_MODEL_CASES  
 範例3說明如何使用 *EXTEND_MODEL_CASES* 選項來提供新的資料，這些資料會加入至現有資料數列的結尾。 新的資料會加入到模型上，而不是取代現有的資料點。  
  
 在下列範例中，NATURAL PREDICTION JOIN 後面的 SELECT 陳述式內會提供新的資料。 您可以使用這個語法來提供新輸入的多個資料列，但是輸入的每一個新資料列都必須有唯一的時間戳記：  
  
```  
SELECT [Model Region],  
    PredictTimeSeries([Forecasting].[Quantity], 5, EXTEND_MODEL_CASES)   
FROM  
    [Forecasting]  
NATURAL PREDICTION JOIN  
    (SELECT  
        1 as [Reporting Date],  
        10 as [Quantity],  
        'M200 Europe' AS [Model Region]  
    UNION SELECT   
        2 as [Reporting Date],  
        15 as [Quantity],  
        'M200 Europe' AS [Model Region]  
) AS T  
WHERE ([Model Region] = 'M200 Europe'  
 OR [Model Region] = 'M200 Pacific')  
```  
  
 由於查詢使用 *EXTEND_MODEL_CASES* 選項，因此 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會對其預測採取下列動作：  
  
-   將兩個新月份的資料加入到模型中來增加定型案例的大小總計。  
  
-   在之前案例資料的結尾開始預測。 因此，前兩個預測代表您剛才加入模型中的新實際銷售資料。  
  
-   根據新擴充的模型，傳回剩餘三個時間配量的新預測。  
  
 下表列出範例 2 查詢的結果。 請注意，針對 M200 Europe 傳回的前兩個值與您提供的新值一模一樣。 這是預設的行為；如果您想要在新資料的結尾之後開始預測，您必須指定開始和結束時間步驟。  
  
 也請注意一點，您並未提供太平洋地區的新資料。 因此，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會針對全部五個時間配量傳回新預測。  
  
 Quantity： M200 歐洲。 EXTEND_MODEL_CASES：  
  
|$TIME|數量|  
|-----------|--------------|  
|7/25/2008 0:00|10|  
|8/25/2008 0:00|15|  
|9/25/2008 0:00|72|  
|10/25/2008 0:00|69|  
|11/25/2008 0:00|68|  
  
 Quantity： M200 太平洋。 EXTEND_MODEL_CASES：  
  
|$TIME|數量|  
|-----------|--------------|  
|7/25/2008 0:00|46|  
|8/25/2008 0:00|44|  
|9/25/2008 0:00|42|  
|10/25/2008 0:00|42|  
|11/25/2008 0:00|38|  
  
## <a name="example-4-returning-statistics-in-a-time-series-prediction"></a>範例 4：傳回時間序列預測的統計資料  
 **PredictTimeSeries**函數不支援做為參數*INCLUDE_STATISTICS* 。 但是，下列查詢可用於傳回時間序列查詢的預測統計資料。 這個方式也可以搭配具有巢狀資料表資料行的模型使用。  
  
 在這個特定模型中，可預測屬性為 Quantity，所以您必須使用 `[Quantity]` 做為 PredictTimeSeries 函數的第一個引數。 如果您的模型使用不同的可預測屬性，可以替代不同的資料行名稱。  
  
```  
SELECT FLATTENED [Model Region],  
(SELECT   
     $Time,  
     [Quantity] as [PREDICTION],   
     PredictVariance([Quantity]) AS [VARIANCE],  
     PredictStdev([Quantity]) AS [STDEV]  
FROM  
      PredictTimeSeries([Quantity], 3) AS t  
) AS t  
FROM Forecasting  
WHERE [Model Region] = 'M200 Europe'  
OR [Model Region] = 'M200 North America'  
```  
  
 範例結果：  
  
|Model Region|t.$TIME|t.PREDICTION|t.VARIANCE|t.STDEV|  
|------------------|-------------|------------------|----------------|-------------|  
|M200 Europe|上午 7/25/2008 12:00:00|121|11.6050581415597|3.40661975300439|  
|M200 Europe|上午 8/25/2008 12:00:00|142|10.678201866621|3.26775180615374|  
|M200 Europe|上午 9/25/2008 12:00:00|152|9.86897842568614|3.14149302493037|  
|M200 North America|上午 7/25/2008 12:00:00|163|1.20434529288162|1.20434529288162|  
|M200 North America|上午 8/25/2008 12:00:00|178|1.65031343900634|1.65031343900634|  
|M200 North America|上午 9/25/2008 12:00:00|156|1.68969399185442|1.68969399185442|  
  
> [!NOTE]  
>  此範例使用 FLATTENED 關鍵字，讓結果更容易呈現在資料表中，不過，如果您的提供者支援階層式資料列集，可以省略 FLATTENED 關鍵字。 如果您省略 FLATTENED 關鍵字，查詢會傳回兩個資料行：第一個資料行包含識別 `[Model Region]` 資料數列的值，而第二個資料行則包含統計資料的巢狀資料表。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [時間序列模型查詢範例](/analysis-services/data-mining/time-series-model-query-examples)   
 [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
