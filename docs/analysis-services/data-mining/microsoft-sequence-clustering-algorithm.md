---
title: "Microsoft 時序群集演算法 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clusters [Analysis Services]
- algorithms [data mining]
- sequence clustering algorithms [Analysis Services]
- sequence [Analysis Services]
ms.assetid: ae779a1f-0adb-4857-afbd-a15543dff299
caps.latest.revision: 49
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 09d9c1909f093547dedd79823a06d9647f0bd6a8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-sequence-clustering-algorithm"></a>Microsoft 時序群集演算法
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法是結合時序分析和叢集的獨特演算法。 您可以使用此演算法來瀏覽資料，其中包含可在 [時序] 中連結的事件。 此演算法會尋找最常見的時序，並執行叢集以尋找類似的時序。 下列範例描述您可能擷取作為機器學習資料的時序類型，以深入了解常見的問題或商務案例：  
  
-   使用者巡覽或瀏覽網站時所產生的點選流或點選路徑  
  
-   列出某個事故之前之事件的記錄，例如硬碟故障或伺服器死結  
  
-   描述客戶將商品放入線上購物車之順序的交易記錄  
  
-   追蹤客戶或病人在某段期間之互動的記錄，以便預測服務取消或其他不好的結果  
  
 這個演算法在許多方面與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 叢集演算法很相似。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法會尋找時序中路徑相似的案例群集，而非包含相似屬性的案例群集。  
  
## <a name="example"></a>範例  
 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] web site collects information about what pages site users visit, and about the order in which the pages are visited. 因為該公司提供線上訂購，客戶必須登入站台。 這樣為公司提供每一個客戶設定檔的點選資訊。 在此資料上使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法，公司可以找出具有類似點選模式或時序的客戶群組或群集。 然後，公司可以使用這些群集來分析使用者在整個網站的移動情形、識別哪些頁面與某項特定產品最有關係，並預測下次最可能再造訪哪些頁面。  
  
## <a name="how-the-algorithm-works"></a>演算法的運作方式  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法是一種混合式演算法，它結合了群集技術與 Markov 鏈結分析，可識別群集及其時序。  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法的其中一項特徵就是它會使用時序資料。 這項資料通常代表資料集內的一系列事件或各狀態之間的轉換，例如特定使用者的一系列產品採購或網頁點選。 此演算法會檢查所有轉換的機率並測量資料集內所有可能時序之間的差異或距離，以便判斷哪些時序最適合當做群集的輸入使用。 在此演算法已經建立候選時序的清單之後，它就會使用此時序資訊當做使用 EM (Expectation Maximization) 之叢集的輸入。  
  
 如需實作的詳細說明，請參閱＜ [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)＞。  
  
## <a name="data-required-for-sequence-clustering-models"></a>時序叢集模型所需的資料  
 當您準備資料以供定型時序叢集模型使用時，應該要了解特定演算法的需求，包括所需的資料量以及資料的使用方式。  
  
 時序叢集模型的需求如下：  
  
-   **單一索引鍵資料行** ：時序叢集模型需要可識別記錄的索引鍵。  
  
-   **時序資料行** ：對於時序資料而言，此模型必須具有包含時序識別碼資料行的巢狀資料表。 此時序識別碼可以是任何可排序的資料類型。 例如，您可以使用網頁識別碼、整數或文字字串，只要資料行可識別時序中的事件即可。 每個時序只能有一個時序識別碼，而且每個模型只能有一種時序。  
  
-   **選擇性非時序屬性** ：此演算法支援加入與時序無關的其他屬性。 這些屬性可以包含巢狀資料行。  
  
 例如，在先前所述的 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 網站範例中，時序叢集模型可能會包含訂單資訊當做案例資料表、每筆訂單之特定客戶的相關人口統計當做非時序屬性，以及包含客戶瀏覽網站或將商品放入購物車之時序的巢狀資料表當做時序資訊。  
  
 如需時序叢集模型所支援內容類型和資料類型的詳細資訊，請參閱 [Microsoft 時序叢集演算法技術參考](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)的＜需求＞一節。  
  
## <a name="viewing-a-sequence-clustering-model"></a>檢視時序叢集模型  
 此演算法所建立的採礦模型會包含資料中最常見時序的描述。 若要瀏覽此模型，您可以使用 **[Microsoft 時序群集檢視器]**。 當您檢視時序叢集模型時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會顯示包含多項轉換的叢集。 您也可以檢視相關的統計資料。 如需詳細資訊，請參閱 [使用 Microsoft 時序叢集檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)。  
  
 如果您想要知道更多詳細資訊，您可以在 [Microsoft 一般內容樹狀檢視器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)中瀏覽此模型。 針對此模型所儲存的內容包括每個節點中所有值的分佈、每個群集的機率，以及有關轉換的詳細資料。 如需詳細資訊，請參閱[時序叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
## <a name="creating-predictions"></a>建立預測  
 在此模型已定型之後，結果會儲存成一組模式。 您可以使用資料中最常見時序的描述來預測新時序的下一個可能步驟。 不過，因為此演算法包含其他資料行，所以您可以使用產生的模型來識別時序資料與非循序輸入之間的關聯性。 例如，如果您將人口統計資料加入至模型，就可以針對特定客戶群組進行預測。 您可以自訂預測查詢，以便傳回變動數目的預測或傳回描述性統計資料。  
  
 如需如何針對資料採礦模型建立查詢的資訊，請參閱 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)。 如需如何在時序叢集模型中使用查詢的範例，請參閱 [時序叢集模型查詢範例](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)。  
  
## <a name="remarks"></a>備註  
  
-   不支援使用預測模型標記語言 (PMML) 來建立採礦模型。  
  
-   支援鑽研。  
  
-   支援 OLAP 採礦模型的使用和資料採礦維度的建立。  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 時序群集演算法技術參考](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [時序群集模型查詢範例](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [使用 Microsoft 時序叢集檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  

