---
title: 建立時間序列預測 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fb22cffa-ac99-4d34-ac4a-9c93068e33e8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 109c4eb07dd34aa5ef3e41d794edfc39ffffcac8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119868"
---
# <a name="creating-time-series-predictions-intermediate-data-mining-tutorial"></a>建立時間序列預測 (中繼資料採礦教學課程)
  在本課之前的工作中，您已經建立一個時間序列模型並瀏覽結果。 根據預設，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 一定會建立一組五個的時間數列模型預測，並將預測值顯示為預測圖表的一部分。 但是，您也可以建立資料採礦延伸模組 (DMX) 預測查詢來建立預測。  
  
 在此工作中，您將會建立預測查詢，此查詢會產生與您在檢視器中所見相同的預測。 此工作假設您已經完成「基本資料採礦教學課程」中的課程，而且很熟悉如何使用預測查詢產生器。 您現在將要學習如何建立時間序列模型特有的查詢。  
  
## <a name="creating-time-series-predictions"></a>建立時間序列預測  
 一般來說，建立預測查詢的第一個步驟是選取採礦模型和輸入資料表。 但是，時間序列模型不需要額外輸入，也能夠進行一般預測。 因此，當您做預測時，不需要指定新的資料來源，除非您要在模型中加入資料或是取代資料。  
  
 在這一課中，您必須指定預測步驟的數目。 您可以指定數列名稱，以取得產品和地區之特定組合的預測。  
  
#### <a name="to-select-a-model-and-input-table"></a>若要選取模型和輸入資料表  
  
1.  在上**採礦模型預測**] 索引標籤的 [資料採礦設計師中**採礦模型**方塊中，按一下**選取模型**。  
  
2.  在 **選取採礦模型**對話方塊方塊中，展開預測結構，選取**預測**從清單中，模型，然後按一下**確定**。  
  
3.  略過**選取輸入資料表** 方塊中。  
  
    > [!NOTE]  
    >  如果是時間序列模型，您不需要指定個別輸入，除非您要執行交叉預測。  
  
4.  在 **來源**在上方格中的資料行，**採礦模型預測**索引標籤上，按一下第一個空白資料列中的資料格，然後選取**預測採礦模型**。  
  
5.  在 **欄位**欄中，選取**Model Region**。  
  
     這個動作會將數列識別碼加入到預測查詢中，以表示此預測會套用到哪一個模型和地區組合。  
  
6.  按一下 下一步中的空白資料列**來源**資料行，然後選取**預測函數**。  
  
7.  在 **欄位**欄中，選取**PredictTimeSeries**。  
  
    > [!NOTE]  
    >  您也可以搭配時間序列模型使用 `Predict` 函數。 但是根據預設，Predict 函數只會針對每一個數列各建立一項預測。 因此，若要指定多個預測步驟，您必須使用**PredictTimeSeries**函式。  
  
8.  在 **採礦模型**窗格中，選取採礦模型資料行，**數量。** 將 Amount 拖曳到**準則/引數**方塊**PredictTimeSeries**您稍早新增的函式。  
  
9. 按一下 **準則/引數**方塊，然後輸入逗號，後面接著**5**，欄位名稱之後。  
  
     中的文字**準則/引數**方塊現在應該會顯示下列：  
  
     `[Forecasting].[Amount],5`  
  
10. 在 **別名**資料行中輸入`PredictAmount`。  
  
11. 按一下 下一步中的空白資料列**來源**資料行，然後選取**預測函數**一次。  
  
12. 在 **欄位**欄中，選取**PredictTimeSeries**。  
  
13. 在 **採礦模型**窗格中選取資料行 Quantity，然後將它拖曳到**準則/引數**第二個方塊**PredictTimeSeries**函式。  
  
14. 按一下 **準則/引數**方塊，然後輸入逗號，後面接著**5**，欄位名稱之後。  
  
     中的文字**準則/引數**方塊現在應該會顯示下列：  
  
     `[Forecasting].[ Quantity],5`  
  
15. 在 **別名**資料行中輸入`PredictQuantity`。  
  
16. 按一下 **切換到查詢結果檢視**。  
  
     查詢的結果會以表格格式顯示。  
  
 請記得，您已經在查詢產生器中建立三種不同類型的結果，其中一種是使用資料行內的值，另外兩種會從預測函數取得預測值。 因此，查詢的結果包含三個不同的資料行。 第一個資料行包含產品和地區組合的清單。 第二和第三個資料行各包含預測結果的巢狀資料表， 每一個巢狀資料表都包含時間步驟和預測值，如下表所示：  
  
 範例結果 (金額截斷為兩個小數位數)：  
  
 **M200 Europe PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|2008 年 7 月 25 日|99978.00|  
|2008 年 8 月 25 日|145575.07|  
|2008 年 9 月 25 日|116835.19|  
|2008 年 10 月 25 日|116537.38|  
|2008 年 11 月 25 日|107760.55|  
  
 **M200 Europe PredictQuantity**  
  
|$TIME|Quantity|  
|-----------|--------------|  
|2008 年 7 月 25 日|52|  
|2008 年 8 月 25 日|67|  
|2008 年 9 月 25 日|58|  
|2008 年 10 月 25 日|57|  
|2008 年 11 月 25 日|54|  
  
 **M200 North America PredictAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|2008 年 7 月 25 日|348533.93|  
|2008 年 8 月 25 日|340097.98|  
|2008 年 9 月 25 日|257986.19|  
|2008 年 10 月 25 日|374658.24|  
|2008 年 11 月 25 日|379241.44|  
  
 **M200 North America PredictQuantity**  
  
|$TIME|Quantity|  
|-----------|--------------|  
|2008 年 7 月 25 日|272|  
|2008 年 8 月 25 日|152|  
|2008 年 9 月 25 日|250|  
|2008 年 10 月 25 日|181|  
|2008 年 11 月 25 日|290|  
  
> [!WARNING]  
>  範例資料庫中使用的日期已在此版本中變更。 如果您使用的是舊版的範例資料，可能會看到不同的結果。  
  
## <a name="saving-the-prediction-results"></a>儲存預測結果  
 您有數個選項可以使用此預測結果。 可以將結果扁平化，並從 [結果] 檢視複製資料，然後貼到 Excel 工作表或其他檔案中。  
  
 為了簡化儲存結果的程序，資料採礦設計師也提供將資料儲存至資料來源檢視的能力。 將結果儲存至資料來源檢視的功能只能在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中使用。 結果只能使用扁平化的格式儲存。  
  
#### <a name="to-flatten-the-results-in-the-results-pane"></a>若要在結果窗格中扁平化結果  
  
1.  在預測查詢產生器中，按一下**切換到查詢設計檢視**。  
  
     此檢視會變更，好讓您手動編輯 DMX 查詢文字。  
  
2.  在 `FLATTENED` 關鍵字之後輸入 `SELECT` 關鍵字。 完整查詢文字應該如下所示：  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    ```  
  
3.  或者，您可以輸入一子句以限制結果，例如以下範例：  
  
    ```  
    SELECT FLATTENED  
      [Forecasting].[Model Region],  
      (PredictTimeSeries([Forecasting].[Amount],5)) as [PredictAmount],  
      (PredictTimeSeries([Forecasting].[Quantity],5)) as [PredictQuantity]  
    FROM  
      [Forecasting]  
    WHERE [Forecasting].[Model Region] = 'M200 North America'   
    OR [Forecasting].[Model Region] = 'M200 Europe'  
  
    ```  
  
4.  按一下 **切換到查詢結果檢視**。  
  
#### <a name="to-export-prediction-query-results"></a>若要匯出預測查詢結果  
  
1.  按一下 **將查詢結果儲存**。  
  
2.  在 [**儲存資料採礦查詢結果**] 對話方塊中，如**資料來源**，選取[!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]。 如果您想要將資料儲存到不同的關聯式資料庫，您也可以建立資料來源。  
  
3.  在 **資料表名稱**資料行中輸入新的暫存資料表名稱，例如**Test Predictions**。  
  
4.  按一下 **[儲存]**。  
  
    > [!NOTE]  
    >  若要檢視您所建立的資料表，請建立與您儲存資料之執行個體的資料庫引擎之間的連接，並建立查詢。  
  
## <a name="conclusion"></a>結論  
 您已經學會如何建立基本的時間序列模型，解譯預測，以及建立預測。  
  
 本教學課程中的剩餘工作是選擇性的，描述進階時間序列預測。 如果您決定要繼續，您將學習如何將新資料加入至模型，以及在擴充數列上建立預測。 您也將會學習如何使用模型中的趨勢，但以新的資料數列取代資料，藉此執行交叉預測。  
  
## <a name="next-lesson"></a>下一課  
 [進階時間序列預測&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/advanced-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [時間序列模型查詢範例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
