---
title: Microsoft 群集演算法 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- segmentation algorithms [Analysis Services]
- nearest neighbor [Data Mining]
- clustering [Data Mining]
- clusters [Analysis Services]
- relationships [Analysis Services], clusters
- algorithms [data mining]
- classification algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
ms.assetid: 92a1e67e-f46e-4960-99b2-4d20f6192fbd
caps.latest.revision: 61
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 74e1a00c89050b632ca01a5f67f734484bff8de7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031323"
---
# <a name="microsoft-clustering-algorithm"></a>Microsoft 群集演算法
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]群集演算法是所提供的分割演算法[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 此演算法使用反覆技巧，將資料集內的案例分成包含類似特性的群集。 這些群集對於瀏覽資料、識別資料的異常及建立預測很有幫助。  
  
 群集模型會識別資料集內，無法透過偶然的邏輯觀察而衍生之關聯性。 例如，您可以從邏輯上看出騎腳踏車上班的人通常不會住在離工作地點很遠的地方。 不過，此演算法可以尋找關於腳踏車通勤者之其他較不明顯的特性。 在下列圖表中，群集 A 代表可能要開車上班的人之資料，而群集 B 代表可能要騎腳踏車上班的人之資料。  
  
 ![通勤者傾向的叢集模式](../media/clustering-example.gif "通勤者傾向的叢集模式")  
  
 群集演算法與其他資料採礦演算法不同，例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法，因為您不必指定可預測資料行就可以建立群集模型。 叢集演算法會從資料中已存在的關聯性以及從演算法識別的群集嚴格地培訓模型。  
  
## <a name="example"></a>範例  
 試想有一群人共用類似的人口統計資訊，而且向 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 公司購買類似產品。 這群人即代表一個資料群集。 數個群集可存在於一個資料庫中。 藉由觀察構成群集的資料行，您可以更清楚地看到資料集內的記錄彼此如何相關。  
  
## <a name="how-the-algorithm-works"></a>演算法的運作方式  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法會先識別資料集內的關聯性，然後依據那些關聯性產生一系列群集。 散佈圖是以視覺方式表示演算法如何將資料分組的有用方式，如下列圖表所示。 散佈圖代表資料集內的所有案例，而每一個案例是圖表上的一個點。 群集會將圖表上的點分組，並說明演算法所識別的關聯性。  
  
 ![在資料集中案例的散佈圖](../media/clustering-plot.gif "集中案例的散佈圖")  
  
 第一次定義群集之後，演算法會計算群集代表點群組的程度，然後嘗試重新定義群組，來建立更能代表資料的群集。 此演算法反覆執行此程序，直到它無法以重新定義群集來改進結果為止。  
  
 您可以藉由選取特定的群集技巧、限制群集的數目上限或變更建立群集所需的支援量，來自訂演算法的作業方式。 如需詳細資訊，請參閱 [Microsoft 群集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)。  
  
## <a name="data-required-for-clustering-models"></a>叢集模型所需的資料  
 當您準備資料以供培訓叢集模型使用時，應該要了解特定演算法的需求，包括所需的資料量及資料的使用方式等。  
  
 叢集模型的需求如下：  
  
-   **單一索引鍵資料行** ：每個模型都必須包含一個能唯一識別每一筆記錄的數值或文字資料行。 不允許複合的索引鍵。  
  
-   **輸入資料行** ：每個模型都至少包含一個輸入資料行，內含用來建置群集的值。 您可以依需求擁有任何數量的輸入資料行，但根據每個資料行中的值數目，加入額外的資料行可能會增加培訓模型所需的時間。  
  
-   **選擇性的可預測資料行** ：演算法不需要使用可預測資料行來建置模型，但您可以加入幾乎任何資料類型的可預測資料行。 可預測資料行的值可用來當做叢集模型的輸入，或者也可以指定只將其用於預測。 例如，如果您想要透過叢集等人口統計資料，例如地區或年齡預測客戶收入，您可以將收入指定為`PredictOnly`並加入所有其他資料行，例如地區或年齡，做為輸入。  
  
 如需叢集模型所支援內容類型和資料類型的詳細資訊，請參閱 [Microsoft 叢集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)的＜需求＞一節。  
  
## <a name="viewing-a-clustering-model"></a>檢視叢集模型  
 若要瀏覽此模型，您可以使用 [Microsoft 群集檢視器]。 在檢視叢集模型時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將叢集顯示在描述叢集關聯性的圖表中，並針對每個叢集提供詳細的設定檔、區分各個叢集的屬性清單以及整個培訓資料集的特性。 如需詳細資訊，請參閱 [使用 Microsoft 叢集檢視器瀏覽模型](browse-a-model-using-the-microsoft-cluster-viewer.md)。  
  
 如果您想要知道更多詳細資訊，您可以在 [Microsoft 一般內容樹狀檢視器](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)中瀏覽此模型。 針對此模型所儲存的內容包括每個節點中所有值的分佈、每個群集的機率及其他資訊。 如需詳細資訊，請參閱[叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)。  
  
## <a name="creating-predictions"></a>建立預測  
 在此模型已培訓之後，結果會儲存成一組模式，供您瀏覽或用來做出預測。  
  
 您可以建立查詢來傳回新資料是否符合已發現之群集的相關預測，或取得有關群集的描述性統計資料。  
  
 如需如何針對資料採礦模型建立查詢的資訊，請參閱 [資料採礦查詢](data-mining-queries.md)。 如需如何在叢集模型中使用查詢的範例，請參閱 [叢集模型查詢範例](clustering-model-query-examples.md)。  
  
## <a name="remarks"></a>備註  
  
-   支援使用預測模型標記語言 (PMML) 來建立採礦模型。  
  
-   支援鑽研。  
  
-   支援 OLAP 採礦模型的使用和資料採礦維度的建立。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法&#40;Analysis Services-資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 群集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)   
 [群集模型的採礦模型內容&#40;Analysis Services-資料採礦&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)   
 [群集模型查詢範例](clustering-model-query-examples.md)  
  
  