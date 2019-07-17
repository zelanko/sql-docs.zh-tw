---
title: Microsoft 羅吉斯迴歸演算法 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d293b386cf02d492e3a78a6cef34396f22277ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68183003"
---
# <a name="microsoft-logistic-regression-algorithm"></a>Microsoft 羅吉斯迴歸演算法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  羅吉斯迴歸演算法是知名的統計技術，可用來模型化二進位結果。  
  
 採用不同的學習技術，就可以在統計研究中以各種方式實作邏輯迴歸。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 羅吉斯迴歸演算法已使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法的變化來實作。 雖然此演算法與類神經網路演算法有許多共同特性，但更容易定型。  
  
 羅吉斯迴歸演算法有一個優點，就是它的彈性極高，可使用任何種類的輸入，並支援數種不同的分析工作：  
  
-   使用人口統計來進行有關結果的預測，例如特定疾病的風險等。  
  
-   瀏覽及衡量促成結果的因素。 例如，尋找影響客戶重覆光顧商店的因素。  
  
-   將文件、電子郵件或其他具有許多屬性的物件分類。  
  
## <a name="example"></a>範例  
 試想有一群人共用類似的人口統計資訊，而且向 Adventure Works 購買產品。 藉由將資料模型化以與特定的結果 (例如購買目標產品) 產生關聯，您可以看出人口統計資訊對某人購買目標產品的可能性有何影響。  
  
## <a name="how-the-algorithm-works"></a>演算法的運作方式  
 羅吉斯迴歸是知名的統計方法，可用來判斷多個因素對一組結果的比重。 Microsoft 實作使用修改過的類神經網路來建立輸入及輸出之間關聯性的模型。 這會評估每個輸入對輸出所造成的效果，而且在完成的模型中會衡量各種輸入。 羅吉斯迴歸之所以如此命名，是因為資料曲線會藉由使用羅吉斯轉換進行壓縮，以最小化極端值的效果。 如需此實作以及如何自訂此演算法的詳細資訊，請參閱 [Microsoft 羅吉斯迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-logistic-regression-models"></a>羅吉斯迴歸模型所需的資料  
 當您準備資料以供羅吉斯迴歸模型使用時，應該要了解特定演算法的需求，包括所需的資料量以及資料的使用方式。  
  
 羅吉斯迴歸模型的需求如下：  
  
 **單一索引鍵資料行** ：每個模型都必須包含一個能唯一識別每一筆記錄的數值或文字資料行。 不允許複合的索引鍵。  
  
 **輸入資料行** ：每個模型都至少包含一個輸入資料行，內含用來當做分析因素的值。 您可以依需求擁有任何數量的輸入資料行，但根據每個資料行中的值數目，加入額外的資料行可能會增加培訓模型所需的時間。  
  
 **至少有一個可預測資料行** ：模型至少必須包含一個任何資料類型的可預測資料行，連續數值資料也包括在內。 可預測資料行的值也可用來當做模型的輸入，或者也可以指定只將其用於預測。 巢狀資料表不可用於可預測的資料行，但可用來當做輸入。  
  
 如需羅吉斯迴歸模型所支援之內容類型和資料類型的詳細資訊，請參閱 [Microsoft 羅吉斯迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)的＜需求＞一節。  
  
## <a name="viewing-a-logistic-regression-model"></a>檢視羅吉斯迴歸模型  
 若要瀏覽此模型，可以使用 Microsoft 類神經網路檢視器，或 Microsoft 一般內容樹狀檢視器。  
  
 當您使用 Microsoft 類神經網路檢視器檢視此模型時，Analysis Services 會顯示對特定結果有影響的因素，並依其重要性排序。 您可以選擇要比較的屬性和值。 如需詳細資訊，請參閱 [使用 Microsoft 類神經網路檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-neural-network-viewer.md)。  
  
 如果想要知道更多詳細資訊，您可以在 Microsoft 一般內容樹狀檢視器中瀏覽此模型的詳細資料。 羅吉斯迴歸模型的模型內容包含可顯示該模型所用之所有輸入的臨界節點，以及可預測屬性的子網路。 如需詳細資訊，請參閱 [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)。  
  
## <a name="creating-predictions"></a>建立預測  
 在模型定型之後，您可以針對模型內容建立查詢以取得迴歸係數和其他詳細資料，也可以使用模型來進行預測。  
  
-   如需如何針對資料採礦模型建立查詢的一般資訊，請參閱 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)。  
  
-   如需羅吉斯迴歸模型使用之查詢的範例，請參閱 [叢集模型查詢範例](../../analysis-services/data-mining/clustering-model-query-examples.md)。  
  
## <a name="remarks"></a>備註  
  
-   不支援鑽研。 這是因為採礦模型中的節點結構不一定會直接對應至基礎資料。  
  
-   不支援建立資料採礦維度。  
  
-   支援 OLAP 採礦模型的使用。  
  
-   不支援使用預測模型標記語言 (PMML) 來建立採礦模型。  
  
## <a name="see-also"></a>另請參閱  
 [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)   
 [Microsoft 羅吉斯迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)   
 [羅吉斯迴歸模型查詢範例](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)  
  
  
