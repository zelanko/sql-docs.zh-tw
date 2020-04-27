---
title: 預測關聯（中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9140c5f2-b340-45a6-9c27-d870d15aafea
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bee5ca4ded1b2fd5cbda0712cb766c825b9d0318
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62472843"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>預測關聯 (中繼資料採礦教學課程)
  當模型經過處理之後，您可以使用與模型中儲存的關聯有關的資訊來建立預測。 在本課程的最後一個工作中，您將會學習如何針對您所建立的關聯模型來建立預測查詢。 此課程假設您已熟悉如何使用預測查詢產生器，而且想要學習如何針對關聯模型來建立預測查詢。 如需如何使用預測查詢產生器的詳細資訊，請參閱[資料採礦查詢介面](../../2014/analysis-services/data-mining/data-mining-query-tools.md)。  
  
## <a name="creating-a-singleton-prediction-query"></a>建立單一預測查詢  
 關聯模型上的預測查詢可能非常實用：  
  
-   根據先前或相關的採購，向客戶推薦項目  
  
-   尋找相關的事件。  
  
-   識別一組交易中或跨一組交易的關聯性。  
  
 若要建立預測查詢，請先選取您想要使用的關聯模型，然後再指定輸入資料。 輸入可以來自外部資料來源 (例如值的清單)，或者您可以建立單一查詢並提供值。  
  
 在此案例中，您會先建立某些單一預測查詢，大概了解預測的運作方式。 然後您會建立批次預測的查詢，讓您用來根據客戶的目前購買項目來做出建議。  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>若要在關聯模型上建立預測查詢  
  
1.  按一下資料採礦設計師的 [**採礦模型預測**] 索引標籤。  
  
2.  在 [**採礦模型**] 窗格中，按一下 [**選取模型**]。 (如果已選取正確的模型，您可以略過這個步驟和下一個步驟)。  
  
3.  在 [**選取採礦模型**] 對話方塊中，展開代表「採礦結構**關聯**」的節點，然後選取模型**關聯**。 按一下 [確定]  。  
  
     現在可以忽略輸入窗格。  
  
4.  在方格中，按一下 [**來源**] 底下的空白資料格，然後選取 [**預測函數]。** 在 [**欄位**] 底下的資料`PredictAssociation`格中，選取。  
  
     您也可以使用**predict**函數來預測關聯。 如果您這樣做，請務必選擇採用資料表資料行做為引數的**Predict**函數版本。  
  
5.  在 [**採礦模型**] 窗格中，選取 [ `vAssocSeqLineItems`嵌套] 資料表，並將它拖曳到方格中，指向`PredictAssociation`函數的 [**準則/引數**] 方塊。  
  
     拖曳資料表和資料行名稱可讓您建立複雜的陳述式，而不會產生語法錯誤。 不過，它會取代資料格的目前內容，其中包括`PredictAssociation`函數的其他選擇性引數。 若要檢視其他引數，您可以暫時將此函數的第二個執行個體加入至方格內以供參考。  
  
6.  按一下 [**準則/引數**] 方塊，並在資料表名稱後面輸入下列文字：`,3`  
  
     [**準則/引數**] 方塊中的完整文字應該如下所示：  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  按一下預測查詢產生器上方角落的 [**結果**] 按鈕。  
  
 預期的結果會包含具有標題**運算式**的單一資料行。 [**運算式**] 資料行包含具有單一資料行和下列三個數據列的嵌套資料表。 因為您未指定輸入值，所以這些預測代表整體而言，此型號最有可能的產品關聯。  
  
|模型|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 接下來，您將使用 [**單一查詢輸入**] 窗格，將產品指定為查詢的輸入，並查看最有可能與該專案相關聯的產品。  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>若要使用巢狀資料表輸入建立單一預測查詢  
  
1.  按一下預測查詢產生器角落的 [**設計**] 按鈕，切換回查詢建立方格。  
  
2.  在 [**採礦模型**] 功能表上，選取 [**單一查詢**]。  
  
3.  在 [**採礦模型**] 對話方塊中，選取 [**關聯**] 模型。  
  
4.  在方格中，按一下 [**來源**] 底下的空白資料格，然後選取 [**預測函數]。** 在 [**欄位**] 底下的資料`PredictAssociation`格中，選取。  
  
5.  在 [**採礦模型**] 窗格中，選取 [ `vAssocSeqLineItems`嵌套] 資料表，並將它拖曳到方格中，指向`PredictAssociation`函數的 [**準則/引數**] 方塊。 在`,3`嵌套的資料表名稱後面輸入，如同上一個程式所示。  
  
6.  在 [**單一查詢輸入**] 對話方塊中，按一下 [ **vAssoc Seq Line Items**] 旁的 [**值**] 方塊，然後按一下 **（...）** 按鈕。  
  
7.  在 [**嵌套資料表輸入**] 對話方塊中， `Touring Tire`選取 [索引**鍵資料行**] 窗格中的，然後按一下 [**加入**]。  
  
8.  按一下 [**結果**] 按鈕。  
  
 結果現在會顯示最有可能與 Touring Tire 產生關聯之產品的預測。  
  
|模型|  
|-----------|  
|Touring Tire Tube|  
|Sport-100|  
|Water Bottle|  
  
 但是，您已經從模型的瀏覽知道 Touring Tire Tube 經常會與 Touring Tire 一起被購買；您比較有興趣知道，您可以向購買這些產品的客戶推薦可以一起購買哪些產品。 您將會變更此查詢，好讓它根據購物籃中的兩個項目預測相關產品。 您也將修改此查詢，為每一個預測的產品增加機率。  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>若要在單一預測查詢中加入輸入和機率  
  
1.  按一下預測查詢產生器角落的 [**設計**] 按鈕，切換回查詢建立方格。  
  
2.  在 [**單一查詢輸入**] 對話方塊中，按一下 [ **vAssoc Seq Line Items**] 旁的 [**值**] 方塊，然後按一下 **（...）** 按鈕。  
  
3.  在 [索引**鍵資料行**] `Touring Tire`窗格中，選取 []，然後按一下 [**新增**]。  
  
4.  在方格中，按一下 [**來源**] 底下的空白資料格，然後選取 [**預測函數]。** 在 [**欄位**] 底下的資料`PredictAssociation`格中，選取。  
  
5.  在 [**採礦模型**] 窗格中，選取 [ `vAssocSeqLineItems`嵌套] 資料表，並將它拖曳到方格中，指向`PredictAssociation`函數的 [**準則/引數**] 方塊。 在`,3`嵌套的資料表名稱後面輸入，如同上一個程式所示。  
  
6.  在 [**嵌套資料表輸入**] 對話方塊中， `Touring Tire Tube`選取 [索引**鍵資料行**] 窗格中的，然後按一下 [**加入**]。  
  
7.  在方格中，于`PredictAssociation`函數的資料列中，按一下 [**準則/引數**] 方塊，然後變更引數以加入引數 INCLUDE_STATISTICS。  
  
     [**準則/引數**] 方塊中的完整文字應該如下所示：  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  按一下 [**結果**] 按鈕。  
  
 巢狀資料表中的結果現在會變更為顯示預測，連同支援和機率。 如需如何解讀這些值的詳細資訊，請參閱[關聯模型的採礦模型內容 &#40;Analysis Services 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)。  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291 .。。|0.252 .。。|  
|Water Bottle|2866|0.192 .。。|0.175 .。。|  
|Patch Kit|2113|0.142 .。。|0.132|  
  
## <a name="working-with-results"></a>使用結果  
 當結果中有許多巢狀資料表時，您可能會想要扁平化結果，以方便檢視。 若要這樣做，您可以手動修改查詢，並加入 `FLATTENED` 關鍵字。  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>若要扁平化預測查詢中的巢狀資料列集  
  
1.  按一下「預測查詢產生器」角落的 [ **SQL** ] 按鈕。  
  
     此方格會變成開啟的窗格，您可以在此窗格中檢視及修改之前由預測查詢產生器所建立的 DMX 陳述式。  
  
2.  在 `SELECT` 關鍵字之後輸入 `FLATTENED`。  
  
     此查詢的完整文字應該如下所示：  
  
    ```  
    SELECT FLATTENED  
      PredictAssociation([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,3)  
    FROM  
      [Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Touring Tire' AS [Model]  
      UNION SELECT 'Touring Tire Tube' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
    ```  
  
3.  按一下預測查詢產生器上方角落的 [**結果**] 按鈕。  
  
 現在您已經手動編輯了查詢，如果您切換回 [設計] 檢視，一定會遺失變更。 如果您想要儲存查詢，可以將您手動建立的 DMX 陳述式複製到文字檔。 當您變更回 [設計] 檢視後，此查詢會還原成之前在 [設計] 檢視中有效的上一個版本。  
  
## <a name="creating-multiple-predictions"></a>建立多個預測  
 假設您想要知道個別客戶的最佳預測 (根據過去購買的產品)。 您可以使用外部資料當做預測查詢的輸入，例如包含客戶識別碼和最近購買之產品的資料表。 其需求是資料表必須已經定義為 Analysis Services 資料來源檢視，而且輸入資料必須包含案例和巢狀資料表 (就像模型中使用的資料表)。 它們不需要同名，但是結構必須類似。 基於這個教學課程的目的，您將會使用此模型定型所在的原始資料表。  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>若要變更預測查詢的輸入方法  
  
1.  在 [**採礦模型**] 功能表中，再次選取 [**單一查詢**]，以清除核取記號。  
  
2.  隨即出現一則錯誤訊息，警告您單一查詢將會遺失。 按一下 [是]  。  
  
     輸入對話方塊的名稱會變更為 [**選取輸入資料表**]。  
  
 因為您對於建立預測查詢來提供客戶識別碼和產品清單當做輸入很感興趣，所以您將會加入客戶資料表當做案例資料表，並加入購買資料表當做巢狀資料表。 然後您會加入預測函數來產生建議。  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>若要使用巢狀資料表輸入來建立預測查詢  
  
1.  在 [採礦模型] 窗格上，選取 [篩選的關聯] 模型。  
  
2.  在 [**選取輸入資料表**] 對話方塊中，按一下 [**選取案例資料表**]。  
  
3.  在 [**選取資料表**] 對話方塊中，針對 [**資料來源**] 選取 [AdventureWorksDW2008]。 在 [**資料表/視圖名稱**] 清單中，選取 [vAssocSeqOrders]，然後按一下 **[確定]**。  
  
     vAssocSeqOrders 資料表就會加入此窗格中。  
  
4.  在 [**選取輸入資料表**] 對話方塊中，按一下 [**選取嵌套資料表**]。  
  
5.  在 [**選取資料表**] 對話方塊中，針對 [**資料來源**] 選取 [AdventureWorksDW2008]。 在 [**資料表/視圖名稱**] 清單中，選取 [vAssocSeqLineItems]，然後按一下 **[確定]**。  
  
     vAssocSeqLineItems 資料表就會加入此窗格中。  
  
6.  在 [**指定嵌套聯結**] 對話方塊中，從案例資料表拖曳 [OrderNumber] 欄位，並將它放到嵌套資料表的 [OrderNumber] 欄位中。  
  
     您也可以按一下 [**新增關聯**性]，並從清單中選取資料行來建立關聯性。  
  
7.  在 [**指定關聯**性] 對話方塊中，確認 [OrderNumber] 欄位已正確對應，然後按一下 **[確定]**。  
  
8.  按一下 **[確定]** 以關閉 [**指定嵌套聯結**] 對話方塊。  
  
     案例資料表和巢狀資料表會在 [設計] 窗格中更新，以顯示連接外部資料行與此模型中之資料行的聯結。 如果關聯性錯誤，您可以用滑鼠右鍵按一下聯結線，然後選取 [**修改連接**] 來編輯資料行對應，也可以用滑鼠右鍵按一下聯結線，然後選取 [**刪除**] 來完全移除關聯性。  
  
9. 將新的資料列加入方格中。 針對 [**來源**]，選取 [ **vAssocSeqOrders 資料表**]。 針對 [**欄位**]，選取 [CustomerKey]。  
  
10. 將新的資料列加入方格中。 針對 [**來源**]，選取 [ **vAssocSeqOrders 資料表**]。 針對 [**欄位**]，選取 [區域]。  
  
11. 將新的資料列加入方格中。 針對 [**來源**] 選取 [**預測函數**]，然後針對`PredictAssociation`[**欄位**] 選取 []。  
  
12. 將 [ `PredictAssociation` vAssocSeqLineItems] 拖曳到資料列的 [**準則/引數**] 方塊中。 按一下 [**準則/引數**] 方塊的結尾，然後輸入下列文字：`INCLUDE_STATISTICS,3`  
  
     [**準則/引數**] 方塊中的完整文字應該是：`[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. 按一下 [**結果**] 按鈕，以查看每個客戶的預測。  
  
 您可嘗試在多個模型上建立類似的預測查詢，以查看篩選是否會變更預測結果。 如需有關建立預測和其他類型查詢的詳細資訊，請參閱[關聯模型查詢範例](../../2014/analysis-services/data-mining/association-model-query-examples.md)。  
  
## <a name="see-also"></a>另請參閱  
 [關聯模型的採礦模型內容 &#40;Analysis Services 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [DMX&#41;的 PredictAssociation &#40;](/sql/dmx/predictassociation-dmx)   
 [使用預測查詢產生器來建立預測查詢](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
