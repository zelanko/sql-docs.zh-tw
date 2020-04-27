---
title: 第3課：處理時間序列結構和模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 16e27b57-eae1-47a7-a02c-47b6ed487d87
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 493d27c9836eb765c655eba5bbb004e4d48cde40
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63042874"
---
# <a name="lesson-3-processing-the-time-series-structure-and-models"></a>第 3 課：處理時間序列結構和模型
  在這一課，您將使用[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)語句，來處理您所建立的時間序列採礦結構和採礦模型。  
  
 當您處理採礦結構時，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會讀取來源資料並建立支援採礦模型的結構。 當您首次建立採礦模型和結構時，一定要進行處理。 如果您在使用 INSERT INTO 時指定採礦結構，陳述式會處理採礦結構及其所有相關聯的採礦模型。  
  
 當您將採礦模型加入至已處理的採礦結構中，就可以使用 `INSERT INTO MINING MODEL` 陳述式，以現有的資料只處理新的採礦模型。  
  
 如需處理採礦模型的詳細資訊，請參閱[&#40;資料採礦&#41;的處理需求和考慮](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
## <a name="insert-into-statement"></a>INSERT INTO 陳述式  
 若要將時間序列的採礦結構及其所有相關聯的採礦模型定型，請使用[INSERT INTO &#40;DMX&#41;](/sql/dmx/insert-into-dmx)語句。 陳述式中的程式碼可分成下列各部份。  
  
-   識別採礦結構  
  
-   列出採礦結構中的資料行  
  
-   定義定型資料  
  
 下面是 `INSERT INTO` 陳述式的一般範例：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
(  
   <mining structure columns>  
)  
OPENQUERY (<source data definition>)  
```  
  
 程式碼的第一行識別您將定型的採礦結構：  
  
```  
INSERT INTO MINING STRUCTURE [<mining structure name>]  
```  
  
 接下來幾行的程式碼指定採礦結構定義的資料行。 您必須列出採礦結構的每一個資料行，且每一個資料行必須對應到來源查詢資料內包含的資料行。  
  
```  
(  
   <mining structure columns>  
)  
```  
  
 程式碼的最後幾行定義將用於定型採礦結構的資料。  
  
```  
OPENQUERY (<source data definition>)  
```  
  
 在這一課，您使用 `OPENQUERY` 來定義來源資料。 如需有關在來源資料上定義查詢之其他方法的詳細資訊，請參閱[&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。  
  
## <a name="lesson-tasks"></a>課程工作  
 您將在這一課執行下列工作：  
  
-   處理採礦結構 Forecasting_MIXED_Structure  
  
-   處理 Forecasting_MIXED、Forecasting_ARIMA 和 Forecasting_ARTXP 等相關聯的採礦模型  
  
## <a name="processing-the-time-series-mining-structure"></a>處理時間序列採礦結構  
  
#### <a name="to-process-the-mining-structure-and-related-mining-models-by-using-insert-into"></a>若要使用 INSERT INTO 來處理採礦結構和相關的採礦模型  
  
1.  在**物件總管**中，以滑鼠右鍵按一下的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]實例，指向 [追加**查詢**]，然後按一下 [ **DMX**]。  
  
     此時會開啟 [查詢編輯器] 且包含新的空白查詢。  
  
2.  將 INSERT INTO 陳述式的一般範例複製到空白查詢中。  
  
3.  取代下列項目：  
  
    ```  
    [<mining structure>]  
    ```  
  
     成為：  
  
    ```  
    Forecasting_MIXED_Structure  
    ```  
  
4.  取代下列項目：  
  
    ```  
    <mining structure columns>  
    ```  
  
     成為：  
  
    ```  
    [ReportingDate],  
    [ModelRegion]   
    ```  
  
5.  取代下列項目：  
  
    ```  
    OPENQUERY(<source data definition>)  
    ```  
  
     成為：  
  
    ```  
    OPENQUERY([Adventure Works DW 2008R2],'SELECT [ReportingDate], [ModelRegion], [Quantity], [Amount]  
    FROM vTimeSeries ORDER BY [ReportingDate]')  
    ```  
  
     來源查詢會參考 IntermediateTutorial [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]範例專案中定義的資料來源。 它使用此資料來源來存取 view vTimeSerie。 此檢視包含要用於定型採礦模型的來源資料。 如果您不熟悉此專案或此視圖，請參閱[第2課：建立預測案例 &#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)。  
  
     現在，完整的陳述式應該如下所示：  
  
    ```  
    INSERT INTO MINING STRUCTURE [Forecasting_MIXED_Structure]  
    (  
       [ReportingDate],[ModelRegion],[Quantity],[Amount])  
    )  
    OPENQUERY(  
    [Adventure Works DW 2008R2],  
    'SELECT [ReportingDate],[ModelRegion],[Quantity],[Amount] FROM vTimeSeries ORDER BY [ReportingDate]'  
    )   
    ```  
  
6.  **在 [檔案**] 功能表上，按一下 [**將 DMXQuery1 另存為**]。  
  
7.  在 [**另存**新檔] 對話方塊中，流覽至適當的資料夾，並`ProcessForecastingAll.dmx`將檔案命名為。  
  
8.  在工具列上，按一下 [**執行**] 按鈕。  
  
 執行完查詢之後，您可以使用已處理的採礦模型建立預測。 在下一課，您將依據您建立的採礦模型來建立幾個預測。  
  
## <a name="next-lesson"></a>下一課  
 [第 4 課：使用 DMX 建立時間序列預測](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;資料採礦&#41;的處理需求和考慮](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)   
 [&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)   
 [&#40;DMX&#41;的 OPENQUERY](/sql/dmx/source-data-query-openquery)  
  
  
