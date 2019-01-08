---
title: 建立預測時序群集模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 94a8d4f9-a76a-49c5-9785-917010359511
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b67ad103cee685ebcbc5455340df9e4d7890e15
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529227"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>在時序群集模型上建立預測 (中繼資料採礦教學課程)
  了解時序群集檢視器中瀏覽它更好的模型之後，您可以使用預測查詢產生器上建立預測查詢**採礦模型預測**資料採礦設計師中的索引標籤。 若要建立預測，請先選取時序群集模型，然後再選取輸入資料。 對於輸入而言，您可以使用外部資料來源，或是建立單一查詢，並在對話方塊中提供值。  
  
 本課程假設您已經熟悉如何使用預測查詢產生器，並想要學習如何建立時序群集模型所特有的查詢。 如需如何使用預測查詢產生器的一般資訊，請參閱[資料採礦查詢介面](../../2014/analysis-services/data-mining/data-mining-query-tools.md)或 資料採礦基本教學課程中，區段[建立預測&#40;資料採礦基本教學課程&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md).  
  
## <a name="creating-predictions-on-the-regional-model"></a>在地區模型上建立預測  
 在此案例中，您會先建立某些單一預測查詢，以了解預測可能會因地區而異的大概情況。  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>若要在時序群集模型上建立單一查詢  
  
1.  按一下 [**採礦模型預測**資料採礦設計師] 索引標籤。  
  
2.  在 **採礦模型**資料行功能表中，選取**單一查詢**。  
  
     **採礦模型** 窗格並**單一查詢輸入**顯示 窗格。  
  
3.  在 **採礦模型**窗格中，按一下**選取模型**。 (如果已經選取時序群集模型，您可以略過這個步驟)。  
  
     **選取採礦模型**對話方塊隨即開啟。  
  
4.  展開代表採礦結構的節點**Sequence Clustering with Region**，並選取模型**Sequence Clustering with Region**。 按一下 [確定] 。 現在請先忽略輸入窗格；當您設定完預測函數之後，您將會指定輸入。  
  
5.  在方格中，按一下下方的空白儲存格**來源**，然後選取**預測函數。** 底下的資料格中**欄位**，選取**PredictSequence**。  
  
    > [!NOTE]  
    >  您也可以使用**Predict**函式。 如果您這樣做，務必選擇的版本**Predict**接受資料表資料行當做引數的函式...  
  
6.  在 **採礦模型**窗格中，選取巢狀的資料表`v Assoc Seq Line Items`，並拖曳到方格中，以**準則/引數**方塊**PredictSequence**函式。  
  
     拖曳資料表和資料行名稱可讓您建立複雜的陳述式，而不會發生語法錯誤。 但是，它會取代目前儲存格的內容，包括其他選擇性引數**PredictSequence**函式。 若要檢視其他引數，您可以暫時將此函數的第二個執行個體加入至方格內以供參考。  
  
7.  按一下 **結果**預測查詢產生器左上角的按鈕。  
  
 預期的結果包含標題的單一資料行**運算式**。 **運算式**資料行包含三個資料行的巢狀的資料表，如下所示：  
  
|$SEQUENCE|Line Number|[模型]|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 這些結果代表什麼意思？ 請記得您並未指定任何輸入。 因此，將會針對整個案例母體擴展進行預測，而且 Analysis Services 會傳回整體上最有可能的預測。  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>將輸入加入至單一預測查詢  
 在此之前，您並未指定任何輸入。 在下一個工作中，您將使用**單一查詢輸入**窗格，即可指定查詢的某些輸入。 首先，您將會使用 [地區] 當做地區時序群集模型的輸入，以判斷是否所有地區的預測時序都是相同的。 然後您將學習如何修改查詢，為每一個預測增加機率，並讓結果扁平化，好讓您更輕鬆地檢視結果。  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>若要針對特定的客戶群組產生預測  
  
1.  按一下 **設計**預測查詢產生器，若要切換回查詢建立方格左上角的按鈕。  
  
2.  在 [**單一查詢輸入**] 對話方塊中，按一下**值**方塊`Region`，然後選取**歐洲**。  
  
3.  按一下 [**結果**] 按鈕，檢視歐洲客戶的預測。  
  
4.  按一下 **設計**預測查詢產生器，若要切換回查詢建立方格左上角的按鈕。  
  
5.  在 [**單一查詢輸入**] 對話方塊中，按一下**值**方塊`Region`，，然後選取**North America**。  
  
6.  按一下 [**結果**] 按鈕，檢視北美地區的客戶的預測。  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>使用自訂運算式增加機率  
 輸出每一個預測的機率稍微複雜一點，因為機率是預測的一個屬性，而且會輸出為巢狀資料表。 如果您很熟悉資料採礦延伸模組 (DMX)，您可以輕鬆地改變查詢，以便在巢狀資料表上加入子 SELECT 陳述式。 但是，您也可以在預測查詢產生器中建立子 SELECT 陳述式，其方式是加入自訂運算式。  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>使用自訂運算式輸出預測之時序的機率  
  
1.  按一下 **設計**預測查詢產生器，若要切換回查詢建立方格左上角的按鈕。  
  
2.  在方格中，在**來源**，按一下新的資料列，然後選取**自訂運算式**。  
  
3.  將底下的方塊**欄位**空白。  
  
4.  針對**別名**，輸入`t`。  
  
5.  在 **準則/引數**方塊中，輸入完整的子 select 陳述式，如下列程式碼範例所示。 請務必包含左右括號。  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  按一下 [**結果**] 按鈕，檢視歐洲客戶的預測。  
  
 結果現在包含兩個巢狀資料表，其中一個包含預測，另一個包含預測的機率。 如果此查詢無效，您可以切換到查詢設計檢視，並檢閱完整的查詢陳述式，應該如下所示：  
  
```  
SELECT  
  PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
  ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
FROM  
  [Sequence Clustering with Region]  
NATURAL PREDICTION JOIN  
(SELECT 'Europe' AS [Region]) AS t  
```  
  
### <a name="working-with-results"></a>使用結果  
 當結果中有許多巢狀資料表時，您可能會想要扁平化結果，以方便檢視。 若要這樣做，您可以手動修改查詢，並加入 `FLATTENED` 關鍵字。  
  
##### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>若要扁平化預測查詢中的巢狀資料列集  
  
1.  按一下 [**查詢**角的預測查詢產生器] 按鈕。  
  
     此方格會變成開啟的窗格，您可以在此窗格中檢視及修改之前由預測查詢產生器所建立的 DMX 陳述式。  
  
2.  在 `SELECT` 關鍵字之後輸入 `FLATTENED`。  
  
     查詢的完整文字應該類似底下所示：  
  
    ```  
    SELECT FLATTENED  
      PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
      ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
    FROM  
      [Sequence Clustering with Region]  
    NATURAL PREDICTION JOIN  
    (SELECT 'Europe' AS [Region]) AS t  
    ```  
  
3.  按一下 **結果**預測查詢產生器左上角的按鈕。  
  
 在您已經手動編輯了查詢之後，如果您切換回 [設計] 檢視，一定會遺失變更。 但是，您可將手動建立的 DMX 陳述式儲存到文字檔中，然後再切換回 [設計] 檢視。 如果您這樣做，此查詢會還原成之前在 [設計] 檢視中有效的上一個版本。  
  
## <a name="creating-predictions-on-the-related-model"></a>在相關模型上建立預測  
 之前的範例使用案例資料表資料行 Region 當做單一預測查詢的輸入，因為您很有興趣知道此模型在地區之間是否有找到任何差異。 但是，在瀏覽此模型之後，您覺得這些差異並不是那麼大，所以無法根據地區自訂產品建議。 您真正有興趣預測的是客戶選取的項目。 因此在隨後的查詢中，您將會使用不包括地區的時序群集模型，為所有客戶產生建議。  
  
### <a name="using-nested-table-columns-as-input"></a>使用巢狀資料表資料行當做輸入  
 首先，您將會建立單一預測查詢，該查詢會使用單一項目當做輸入，並傳回下一個最有可能的項目。 若要取得這種類型的預測，您必須使用巢狀資料表資料行當做輸入值。 這是因為您所預測的屬性 Model 是巢狀資料表的一部分。 Analysis Services 會提供**巢狀資料表輸入**對話方塊，幫助您輕鬆地建立預測查詢，在巢狀資料表屬性，利用預測查詢產生器 」。  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>若要使用巢狀資料表當做預測的輸入  
  
1.  按一下 **設計**預測查詢產生器，若要切換回查詢建立方格左上角的按鈕。  
  
2.  在 **單一查詢輸入** 對話方塊中，按一下**值**方塊`Region`，，然後選取 空的資料列，以清除此欄位的輸入。  
  
3.  在 **單一查詢輸入** 對話方塊中，按一下**值**方塊`vAssocSeqLineItems`，然後按一下 （...） 按鈕。  
  
4.  在 [**巢狀資料表輸入**] 對話方塊中，按一下**新增**。  
  
5.  在新的資料列中，按一下 底下的方塊`Model`，並從清單中選取 Touring Tire。 按一下 [確定] 。  
  
6.  按一下 **結果**按鈕，以檢視預測。  
  
 此模型會針對選擇 Touring Tire 當做第一個項目的所有客戶建議以下的項目。 您已經從模型的瀏覽知道，客戶經常會同時購買 Touring Tire 和 Touring Tire Tube 產品，所以這些建議似乎不錯。  
  
|$SEQUENCE|Line Number|[模型]|  
|---------------|-----------------|-----------|  
|1||Touring Tire Tube|  
|2||Sport-100|  
|3||Long-Sleeve Logo Jersey|  
  
### <a name="creating-a-bulk-prediction-query-using-nested-table-inputs"></a>使用巢狀資料表輸入建立大量預測查詢  
 現在，此模型建立的預測種類可供您在建議中使用，您對於這樣的結果感到滿意，而且您將會建立一個對應至外部資料來源的預測查詢。 該資料來源將會提供代表目前產品的值。 因為您對於建立預測查詢來提供客戶識別碼和產品清單當做輸入很感興趣，所以您將會加入客戶資料表當做案例資料表，並加入購買資料表當做巢狀資料表。 然後您會跟之前一樣加入預測函數來產生建議。  
  
 這是您在第 3 課中用來針對購物籃分析建立預測的相同程序；但是在時序群集模型中，預測也需要訂單當做輸入。  
  
##### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>若要使用巢狀資料表輸入來建立預測查詢  
  
1.  在 **採礦模型**窗格中，選取 時序群集模型，如果未選取。  
  
2.  在 [**選取輸入資料表**] 對話方塊中，按一下**選取案例資料表**。  
  
3.  在 [**選取資料表**] 對話方塊中，針對資料來源，選取 [訂單]。 在 **資料表/檢視名稱**清單中，選取 vAssocSeqOrders，然後按一下**確定**。  
  
4.  在 [**選取輸入資料表**] 對話方塊中，按一下**選取巢狀資料表**。  
  
5.  在 [**選取資料表**] 對話方塊中，如**資料來源**，選取 [訂單]。 在 **資料表/檢視名稱**清單中，選取 vAssocSeqLineItems，然後再按**確定**。  
  
     Analysis Services 將會嘗試偵測關聯性，並在資料類型相符且資料行名稱類似時自動建立關聯性。 如果它會建立此關聯性錯誤，您可以以滑鼠右鍵按一下聯結線，並選取**修改連接**若要編輯資料行對應，或者您可以以滑鼠右鍵按一下聯結線並選取**刪除**至完全移除關聯性。 在此案例中，因為資料表已經在資料來源檢視中聯結，所以這些關聯性會自動加入到 [設計] 窗格中。  
  
6.  將新的資料列加入方格中。 針對**來源**，選取 [Assocseqorders]，並針對**欄位**，選取 [customerkey]。  
  
7.  將新的資料列加入方格中。 針對**來源**，選取**預測函數**，以及**欄位**，選取**PredictSequence**。  
  
8.  將 vAssocSeqLineItems 拖曳到**準則/引數** 方塊中。 按一下 在結尾**準則/引數**方塊，然後輸入下列的引數： `2`。  
  
     中的完整文字**準則/引數**方塊應該是： `[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. 按一下 **結果**按鈕，以檢視每個客戶的預測。  
  
 您已經完成時序群集模型上的教學課程。  
  
## <a name="next-steps"></a>後續步驟  
 如果您已完成所有章節[中繼資料採礦教學課程&#40;Analysis Services-Data Mining&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)下, 一步可能要學習如何使用資料採礦延伸模組 (DMX) 陳述式來建立模型和產生預測。 如需詳細資訊，請參閱[建立及查詢資料採礦模型使用 DMX:教學課程&#40;Analysis Services-資料採礦&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)。  
  
 如果您很熟悉程式設計概念，您也可以使用分析管理物件 (AMO) 來以程式設計方式處理資料採礦物件。 如需詳細資訊，請參閱 [AMO 資料採礦類別](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes)。  
  
## <a name="see-also"></a>另請參閱  
 [Sequence Clustering Model Query Examples](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [時序叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
