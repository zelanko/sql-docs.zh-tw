---
title: 時間序列預測使用更新的資料 （中繼資料採礦教學課程） |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: af73681d-ce1c-4b6e-b195-6df3d2fb5275
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3478a52657e26fa8e376e88bc83a5c4d9813cdc8
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312356"
---
# <a name="time-series-predictions-using-updated-data-intermediate-data-mining-tutorial"></a>使用更新資料執行時間序列預測 (中繼資料採礦教學課程)
    
## <a name="creating-predictions-using-the-extended-sales-data"></a>使用擴充銷售資料建立預測  
 在本課中，您將建立一個預測查詢，這個查詢會將新的銷售資料加入至模型中。 透過使用新資料擴充模型，您可以取得包含最新資料點的最新預測。  
  
 建立使用新資料的時間序列預測很簡單： 只需要將 EXTEND_MODEL_CASES 參數至[PredictTimeSeries &#40;DMX&#41; ](/sql/dmx/predicttimeseries-dmx)函式，指定新的資料來源，並指定多少您想要取得的預測。  
  
> [!WARNING]  
>  EXTEND_MODEL_CASES 參數是選擇性的；當您透過聯結新資料做為輸入來建立時間序列預測查詢時，預設就會擴充模型。  
  
#### <a name="to-build-the-prediction-query-and-add-new-data"></a>若要建立預測查詢及加入新資料  
  
1.  如果模型尚未開啟，按兩下預測結構，然後在 資料採礦設計師中，按一下 **採礦模型預測** 索引標籤。  
  
2.  在**採礦模型**窗格中，應該已經選取預測模型。 如果未選取，按一下**選取模型**，然後選取 模型，預測。  
  
3.  在**選取輸入資料表**] 窗格中，按一下 [**選取案例資料表**。  
  
4.  在**選取資料表**對話方塊方塊中，選取資料來源， [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。  
  
     從資料來源檢視的清單中，選取 NewSalesData，然後再按一下**確定**。  
  
5.  以滑鼠右鍵按一下設計區域的介面，然後選取**修改連接**。  
  
6.  使用**修改對應**對話方塊方塊中，將模型中的資料行對應至外部資料中的資料行，如下所示：  
  
    -   將採礦模型中的 ReportingDate 資料行對應 NewDate 中的資料行的輸入資料。  
  
    -   將採礦模型中的 Amount 資料行對應 NewAmount 中的資料行的輸入資料。  
  
    -   將採礦模型中的 Quantity 資料行對應 NewQty 中的資料行的輸入資料。  
  
    -   將 ModelRegion 資料行與採礦模型中的對應數列中的資料行的輸入資料。  
  
7.  現在，您將建立預測查詢。  
  
     首先，將資料行加入到預測查詢中，以輸出套用此預測的數列。  
  
    1.  在方格中，按一下第一個空白資料列，在**來源**，然後選取 預測。  
  
    2.  在**欄位**資料行中，選取 Model Region 和**別名**，型別`Model Region`。  
  
8.  接著加入及編輯預測函數。  
  
    1.  按一下空白的資料列，然後在**來源**，選取**預測函數**。  
  
    2.  如**欄位**，選取**PredictTimeSeries**。  
  
    3.  如**別名**，型別**Predicted Values**。  
  
    4.  拖曳 [數量] 欄位從**採礦模型**窗格將**準則/引數**資料行。  
  
    5.  在**準則/引數**資料行中，於欄位名稱之後輸入下列文字： **5，EXTEND_MODEL_CASES**  
  
         完整文字**準則/引數**文字方塊應，如下所示： `[Forecasting].[Quantity],5,EXTEND_MODEL_CASES`  
  
9. 按一下**結果**檢閱結果。  
  
     預測會在 7 月開始 (原始資料結尾後的第一個時間配量) 並在 11 月結束 (原始資料結尾後的第五個時間配量)。  
  
 您可以看到，若要有效地使用這類預測查詢，需要知道舊資料何時結束，以及新資料中有多少時間配量。  
  
 例如，在此模型中，原始資料數列在 6 月結束，而資料是 7 月、8 月和 9 月這些月份的資料。  
  
 使用 EXTEND_MODEL_CASES 的預測一定開始於原始資料數列的結尾。 因此，如果您只要取得未知月份的預測，則需要指定預測的起點和終點。 這兩個值都是以開始於舊資料結尾的時間配量數目指定。  
  
 下列程序示範此做法。  
  
### <a name="change-the-start-and-end-points-of-the-predictions"></a>變更預測的起點和終點  
  
1.  在預測查詢產生器中，按一下**查詢**切換到 DMX 檢視。  
  
2.  找出包含 PredictTimeSeries 函數的 DMX 陳述式，加以變更，如下所示：  
  
     `PredictTimeSeries([Forecasting 12].[Quantity],4,6,EXTEND_MODEL_CASES)`  
  
3.  按一下**結果**檢閱結果。  
  
     現在預測會在 10 月開始 (從原始資料結尾算起的第四個時間配量) 並在 12 月結束 (從原始資料結尾算起的第六個時間配量)。  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [時間序列預測使用取代資料&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [時間序列模型的採礦模型內容&#40;Analysis Services-資料採礦&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
