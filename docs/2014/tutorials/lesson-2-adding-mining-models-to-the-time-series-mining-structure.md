---
title: 第 2 課： 將採礦模型加入至時間序列採礦結構 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 75c2a74b-21ce-44fb-a26b-68be4c685c12
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cee3d839ae7a7bcce62c8a3a1d2f7cb62b1155e2
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312486"
---
# <a name="lesson-2-adding-mining-models-to-the-time-series-mining-structure"></a>第 2 課：將採礦模型加入時間序列採礦結構中
  在這一課，您將會加入新的採礦模型，您在建立採礦結構[第 1 課： 建立時間序列採礦模型和採礦結構](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)。  
  
## <a name="alter-mining-structure-statement"></a>ALTER MINING STRUCTURE 陳述式  
 若要將新的採礦模型加入至現有的採礦結構中，您使用 [ALTER MINING STRUCTURE &#40;DMX&#41;] （(~/dmx/alter-mining-structure-dmx.md) 陳述式。 陳述式中的程式碼可分成下列各部份：  
  
-   識別採礦結構  
  
-   命名採礦模型  
  
-   定義索引鍵資料行  
  
-   定義可預測的資料行  
  
-   指定演算法和任何參數變更  
  
 以下是 ALTER MINING STRUCTURE 陳述式的一般範例：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
ADD MINING MODEL [<mining model name>]  
   ([<key columns>],  
    <mining model columns>  
   )  
USING <algorithm name>([<algorithm parameters>])  
[WITH DRILLTHROUGH]  
```  
  
 程式碼的第一行會識別將加入採礦模型的現有採礦結構：  
  
```  
ALTER MINING STRUCTURE [<mining structure name>]  
```  
  
 程式碼的下一行命名要加入採礦結構中的採礦模型：  
  
```  
ADD MINING MODEL [<mining model name>]  
```  
  
 在 DMX 中的物件命名的詳細資訊，請參閱[識別碼&#40;DMX&#41;](/sql/dmx/identifiers-dmx)。  
  
 接下來幾行的程式碼定義採礦結構中將由採礦模型使用的資料行：  
  
```  
[<key columns>],  
<mining model columns>  
```  
  
 您只能使用已存在於採礦結構中的資料行，且清單中的第一個資料行必須是採礦結構中的索引鍵資料行。  
  
 程式碼的下一行會定義產生採礦模型的採礦演算法，以及您可以在演算法上設定的演算法參數，並指定您是否可以從採礦模型向下鑽研到定型案例中的檢視詳細資料：  
  
```  
USING <algorithm name>([<algorithm parameters>])  
WITH DRILLTHROUGH  
```  
  
 如需您可以調整之演算法參數的詳細資訊，請參閱[Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
 您可以使用下列語法來指定採礦模型中要用於預測的資料行：  
  
```  
<mining model column> PREDICT  
```  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   將新的時間序列採礦模型加入到結構中。  
  
-   變更演算法參數，以使用不同的分析和預測方法。  
  
## <a name="adding-an-arima-time-series-model-to-the-structure"></a>將 ARIMA 時間序列模型加入到結構中  
 第一個步驟是將新的預測採礦模型加入到現有的結構中。 根據預設，[!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法會使用兩個演算法 (ARIMA 和 ARTXP) 建立時間序列採礦模型，並混和結果。 但是，您可以指定所要使用的單一演算法，或是指定確切的演算法混和。 在這個步驟中，您將會加入只使用 ARIMA 演算法的新模型。 此演算法已針對長期預測而最佳化。  
  
#### <a name="to-add-an-arima-time-series-mining-model"></a>若要加入 ARIMA 時間序列採礦模型  
  
1.  在**物件總管] 中**，以滑鼠右鍵按一下執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，指向**新查詢**，然後按一下 [ **DMX**開啟查詢編輯器以及新的空白查詢。  
  
2.  將 ALTER MINING STRUCTURE 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    <mining structure name>   
    ```  
  
     成為：  
  
    ```  
    [Forecasting_MIXED_Structure]  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining model name>   
    ```  
  
     成為：  
  
    ```  
    Forecasting_ARIMA  
    ```  
  
5.  取代下列項目：  
  
    ```  
    <key columns>,  
    ```  
  
     成為：  
  
    ```  
    [ReportingDate],  
    [ModelRegion]  
    ```  
  
     請注意，您不需要重複您在 CREATE MINING MODEL 陳述式中所提供的任何資料類型或內容類型資訊，因為這項資訊已經儲存在採礦結構中。  
  
6.  取代下列項目：  
  
    ```  
    <mining model columns>  
    ```  
  
     成為：  
  
    ```  
    ([Quantity] PREDICT,  
    [Amount] PREDICT  
    )  
    ```  
  
7.  取代下列項目：  
  
    ```  
    USING <algorithm name>([<algorithm parameters>])   
    [WITH DRILLTHROUGH]  
    ```  
  
     成為：  
  
    ```  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
     現在，產生的陳述式應該如下所示：  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARIMA]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARIMA')  
    WITH DRILLTHROUGH  
    ```  
  
8.  在**檔案**功能表上，按一下 **另存 DMXQuery1.dmx 為**。  
  
9. 在**存**對話方塊中，瀏覽至適當的資料夾，並將檔案`Forecasting_ARIMA.dmx`。  
  
10. 在工具列上，按一下 [ **Execute** ] 按鈕。  
  
## <a name="adding-an-artxp-time-series-model-to-the-structure"></a>將 ARTXP 時間序列模型加入到結構中  
 ARTXP 演算法是 SQL Server 2005 中的預設時間序列演算法，而且已針對長期預測而最佳化。 為了使用所有的這三種時間序列演算法來比較預測，您將會再加入一個根據 ARTXP 演算法的模型。  
  
#### <a name="to-add-an-artxp-time-series-mining-model"></a>若要加入 ARTXP 時間序列採礦模型  
  
1.  複製下列程式碼，並貼入空白查詢視窗中。  
  
     請注意，除了新採礦模型的名稱及 FORECAST_METHOD 參數值以外，您不需要變更任何項目。  
  
    ```  
    ALTER MINING STRUCTURE [Forecasting_MIXED_Structure]  
    ADD MINING MODEL [Forecasting_ARTXP]  
       (  
       ([ReportingDate],  
        [ModelRegion],  
        ([Quantity] PREDICT,  
        [Amount] PREDICT  
       )   
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = .08, FORECAST_METHOD = 'ARTXP')  
    WITH DRILLTHROUGH  
    ```  
  
2.  在**檔案**功能表上，按一下 **另存 DMXQuery1.dmx 為**。  
  
3.  在**存**對話方塊中，瀏覽至適當的資料夾，並將檔案`Forecasting_ARTXP.dmx`。  
  
4.  在工具列上，按一下 [ **Execute** ] 按鈕。  
  
 在下一課，您將處理所有的模型和採礦結構。  
  
## <a name="next-lesson"></a>下一課  
 [第 3 課： 處理時間序列結構和模型](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
