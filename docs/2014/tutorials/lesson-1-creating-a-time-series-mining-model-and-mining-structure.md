---
title: 第1課：建立時間序列的採礦模型和採礦結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b201f2b8-9ab5-425b-9ff3-fe321a60a7b7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2513bc3837dd224f6561eb0015ced538ea3add8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62678444"
---
# <a name="lesson-1-creating-a-time-series-mining-model-and-mining-structure"></a>第 1 課：建立時間序列採礦模型和採礦結構
  在這一課，您將建立一個採礦模型，好讓您根據歷程記錄資料預測一段時間的值。 當您建立此模型時，基礎結構將會自動產生而且可用來當做其他採礦模型的基礎。  
  
 本課假設您已經熟悉預測模型及 Microsoft 時間序列演算法的需求。 如需詳細資訊，請參閱 [Microsoft 時間序列演算法](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)。  
  
## <a name="create-mining-model-statement"></a>CREATE MINING MODEL 陳述式  
 若要直接建立採礦模型並自動產生基礎的採礦結構，您可以使用[&#40;DMX&#41;語句建立採礦模型](/sql/dmx/create-mining-model-dmx)。 陳述式中的程式碼可分成下列各部份：  
  
-   命名模型  
  
-   定義時間戳記  
  
-   定義選擇性數列索引鍵資料行  
  
-   定義可預測的屬性  
  
 以下是 CREATE MINING MODEL 陳述式的一般範例：  
  
```  
CREATE MINING MODEL [<Mining Structure Name>]  
(  
   <key columns>,  
   <predictable attribute columns>  
)  
USING <algorithm name>([parameter list])  
WITH DRILLTHROUGH  
```  
  
 此程式碼的第一行會定義採礦模型的名稱：  
  
```  
CREATE MINING MODEL [Mining Model Name]  
```  
  
 Analysis Services 會自動產生基礎結構的名稱，其方式是在模型名稱後附加 "_structure"，如此可確保結構名稱與模型名稱一樣保持唯一。 如需在 DMX 中命名物件的詳細資訊，請參閱[dmx&#41;&#40;的識別碼](/sql/dmx/identifiers-dmx)。  
  
 此程式碼的下一行會定義採礦模型的索引鍵資料行，其中時間序列模型的案例會唯一識別來源資料中的時間步驟。 在資料行名稱和資料類型之後使用 `KEY TIME` 關鍵字識別時間步驟。 如果時間序列模型具有個別的數列索引鍵，將會使用 `KEY` 關鍵字來識別它。  
  
```  
<key columns>  
```  
  
 此程式碼的下一行是用來定義此模型中將要預測的資料行。 在單一採礦模型中可以有多個可預測屬性。 當有多個可預測屬性時，Microsoft 時間序列演算法會針對每一個數列產生個別的分析：  
  
```  
<predictable attribute columns>  
```  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   建立新的空白查詢  
  
-   改變查詢來建立採礦模型  
  
-   執行查詢  
  
## <a name="creating-the-query"></a>建立查詢  
 第一步是連接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體，並在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中建立新的 DMX 查詢。  
  
#### <a name="to-create-a-new-dmx-query-in-sql-server-management-studio"></a>若要在 SQL Server Management Studio 中建立新的 DMX 查詢  
  
1.  開啟 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 [**連接到伺服器**] 對話方塊的 [**伺服器類型**] 中，選取 [ **Analysis Services**]。 在 [**伺服器名稱**] `LocalHost`中，輸入，或您想要[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]在本課程中連接之實例的名稱。 按一下 [ **連接**]。  
  
3.  在**物件總管**中，以滑鼠右鍵按一下的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例，指向 [追加**查詢**]，然後按一下 [ **DMX**]。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
## <a name="altering-the-query"></a>改變查詢  
 下一步是修改 CREATE MINING MODEL 陳述式來建立預測用的採礦模型，連同它的基礎採礦結構。  
  
#### <a name="to-customize-the-create-mining-model-statement"></a>若要自訂 CREATE MINING MODEL 陳述式  
  
1.  在查詢編輯器中，將 CREATE MINING MODEL 陳述式的一般範例複製到空白查詢中。  
  
2.  取代下列項目：  
  
    ```  
    [mining model name]   
    ```  
  
     取代為  
  
    ```  
    [Forecasting_MIXED]  
    ```  
  
3.  取代下列項目：  
  
    ```  
    <key columns>  
    ```  
  
     取代為  
  
    ```  
    [Reporting Date] DATE KEY TIME,  
    [Model Region] TEXT KEY  
    ```  
  
     
  `TIME KEY` 關鍵字指示 ReportingDate 資料行包含用來排序值的時間步驟值。 時間步驟可以是日期和時間、整數，或是任何排序的資料類型，只要這些值是唯一而且可排序資料即可。  
  
     
  `TEXT` 和 `KEY` 關鍵字指示 ModelRegion 資料行包含其他數列索引鍵。 您只能有一個數列索引鍵，而且此資料行中的值必須相異。  
  
4.  取代下列項目：  
  
    ```  
    < predictable attribute columns> )  
    ```  
  
     取代為  
  
    ```  
    [Quantity] LONG CONTINUOUS PREDICT,  
    [Amount] DOUBLE CONTINUOUS PREDICT  
    )  
    ```  
  
5.  取代下列項目：  
  
    ```  
    USING <algorithm name>([parameter list])  
    WITH DRILLTHROUGH  
    ```  
  
     取代為  
  
    ```  
    USING Microsoft_Time_Series(AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
    ```  
  
     演算法參數 `AUTO_DETECT_PERIODICITY` = 0.8 指示您希望此演算法偵測資料中的循環。 將這個值設定為越接近 1，就會探索更多的模式，但是會減緩處理的速度。  
  
     演算法參數 `FORECAST_METHOD` 指示您是否想要使用 ARTXP、ARIMA 或混用這兩者來分析資料。  
  
     
  `WITH DRILLTHROUGH` 關鍵字指定您希望在完成此模型之後，能夠檢視來源資料中的詳細統計資料。 如果您想要使用 Microsoft 時間序列檢視器來瀏覽此模型，必須加入這個子句。 預測時則不需要使用它。  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    CREATE MINING MODEL [Forecasting_MIXED]  
         (  
        [Reporting Date] DATE KEY TIME,  
        [Model Region] TEXT KEY,  
        [Quantity] LONG CONTINUOUS PREDICT,  
        [Amount] DOUBLE CONTINUOUS PREDICT  
        )  
    USING Microsoft_Time_Series (AUTO_DETECT_PERIODICITY = 0.8, FORECAST_METHOD = 'MIXED')  
    WITH DRILLTHROUGH  
  
    ```  
  
6.  **在 [檔案**] 功能表上，按一下 [**將 DMXQuery1 另存為**]。  
  
7.  在 [**另存**新檔] 對話方塊中，流覽至適當的資料夾，並`Forecasting_MIXED.dmx`將檔案命名為。  
  
## <a name="executing-the-query"></a>執行查詢  
 最後的步驟是執行查詢。 在建立及儲存查詢之後，需要執行它，才能在伺服器上建立採礦模型和它的採礦結構。 如需在 [查詢編輯器] 中執行查詢的詳細資訊，請參閱[資料庫引擎查詢編輯器 &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)。  
  
#### <a name="to-execute-the-query"></a>若要執行查詢  
  
-   在 [查詢編輯器] 的工具列上，按一下 [**執行**]。  
  
     查詢的狀態會在語句完成執行之後，顯示在 [查詢編輯器] 底部的 [**訊息**] 索引標籤中。 訊息應該顯示如下：  
  
    ```  
    Executing the query   
    Execution complete  
    ```  
  
     現在伺服器上已存在名為**Forecasting_MIXED_Structure**的新結構，以及相關的「採礦模型**Forecasting_MIXED**。  
  
 在下一課中，您會將「採礦模型」新增至您剛才建立的**Forecasting_MIXED**的「採礦結構」中。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：將採礦模型加入時間序列採礦結構中](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
  
## <a name="see-also"></a>另請參閱  
 [時間序列模型的採礦模型內容 &#40;Analysis Services 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)   
 [Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
