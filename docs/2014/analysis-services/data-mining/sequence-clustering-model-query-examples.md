---
title: 時序群集模型查詢範例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- sequence clustering algorithms [Analysis Services]
- content queries [DMX]
- sequence [Analysis Services]
ms.assetid: 64bebcdc-70ab-43fb-8d40-57672a126602
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d871ba87147f24fdd60c9effe5f279d9ea355db1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082916"
---
# <a name="sequence-clustering-model-query-examples"></a>時序叢集模型查詢範例
  當您針對資料採礦模型建立查詢時，可以建立內容查詢來提供有關模型中排序之資訊的詳細資料，或是建立預測查詢來使用模型中的模式，根據所提供的新資料進行預測。 對於時序群集模型，內容查詢通常會提供找到之群集的其他詳細資料，或提供這些群集中的轉換。 您也可以使用查詢來擷取有關模型的中繼資料。  
  
 時序群集模型的預測查詢通常會根據轉換的時序、包含在模型中的非時序屬性，或者時序與非時序屬性的組合，做出建議。  
  
 本節說明如何針對以 Microsoft 時序群集演算法為基礎的模型來建立查詢。 如需建立查詢的一般資訊，請參閱 [資料採礦查詢](data-mining-queries.md)。  
  
 **內容查詢**  
  
 [使用資料採礦架構資料列集傳回模型參數](#bkmk_Query1)  
  
 [取得狀態的序列清單](#bkmk_Query2)  
  
 [使用系統預存程式](#bkmk_Query3)  
  
 **預測查詢**  
  
 [預測下一個狀態或狀態](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a>尋找時序群集模型的相關資訊  
 若要在採礦模型的內容上建立有意義的查詢，您必須了解模型內容的結構，以及哪一種節點類型會儲存那一種資訊。 如需詳細資訊，請參閱 [時序叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-sequence-clustering-models.md)。  
  
###  <a name="bkmk_Query1"></a>範例查詢1：使用資料採礦架構資料列集傳回模型參數  
 您可以藉由查詢資料採礦結構描述資料列集來尋找有關模型的各種資訊，包括基本中繼資料、此模型建立的日期和時間、上次處理此模型的日期和時間、此模型所依據之採礦結構的名稱，以及當做可預測屬性使用的資料行。  
  
 下列查詢會傳回用於建立和定型模型 `[Sequence Clustering]`的參數。 您可以在＜ [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md)＞的第 5 課中建立此模型。  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 範例結果︰  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 請注意，此模型是使用 CLUSTER_COUNT 的預設值 10 來建立的。 當您針對 CLUSTER_COUNT 指定非零的群集數目時，此演算法會將此數目視為要尋找之約略群集數目的提示。 不過，在分析時，此演算法可能會找到更多或更少的群集。 在此情況下，此演算法會發現 15 個群集最適合定型資料。 因此，已完成模型的參數值清單會報告此演算法決定的群集計數，而不是建立模型時傳入的值。  
  
 此行為與讓演算法決定最佳的群集數目有什麼不同？ 您可以做一個試驗，建立另一個使用這個相同資料的群集模型，但將 CLUSTER_COUNT 設定為 0。 此時，演算法會偵測到 32 個群集。 因此，您可以透過使用 CLUSTER_COUNT 的預設值 10 來限制結果的數目。  
  
 預設使用 10 這個值，因為減少群集數目會讓多數人更容易瀏覽與了解資料中的群組。 不過，每個模型和資料集都不同。 您可能想要試驗不同的群集數目以查看哪個參數值會產生最精確的模型。  
  
###  <a name="bkmk_Query2"></a>範例查詢2：取得狀態的序列清單  
 採礦模型內容會將定型資料中找到的時序儲存為結合其他所有相關狀態之清單的第一個狀態。 第一個狀態會當做時序的標籤使用，而後續的相關狀態則稱為轉換。  
  
 例如，下列查詢會在時序分組到群集之前，傳回模型中第一個狀態的完整清單。  您可以傳回模型根節點當做父系 (PARENT_UNIQUE_NAME = 0) 之時序 (NODE_TYPE = 13) 的清單，藉以取得此清單。 FLATTENED 關鍵字會讓結果更容易讀取。  
  
> [!NOTE]  
>  資料行 PARENT_UNIQUE_NAME、[支援] 與 [機率] 的名稱必須括在括號內，以便與同名的保留關鍵字區別。  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 部分結果：  
  
|NODE_UNIQUE_NAME|產品 1|時序支援|時序機率|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Missing|0|#######|  
|1081327|All-Purpose Bike Stand|17|0.00111|  
|1081327|Bike Wash|64|0.00418|  
|1081327|(資料列 4-36 省略)|||  
|1081327|Women's Mountain Shorts|506|0.03307|  
  
 模型中的時序清單永遠依字母的遞增順序排序。 時序的排序相當重要，因為您可以查看時序的排序數字尋找相關的轉換。 
  `Missing` 值一定是轉換 0。  
  
 例如，在先前的結果中，產品 "Women's Mountain Shorts" 在模型中是時序編號 37。 您可以使用該資訊檢視在 "Women's Mountain Shorts" 後曾經購買的所有產品。  
  
 若要這樣做，首先，您要參考先前查詢中，針對 NODE_UNIQUE_NAME 傳回的值，藉以取得包含模型所有時序之節點的識別碼。 然後您要將此值傳遞到查詢中，當做父節點的識別碼，藉以僅取得此節點中所包含的轉換，而此節點中恰好就包含模型之所有時序的清單。 不過，如果您要查看特定群集之轉換的清單，您可以傳入叢集節點的識別碼，然後僅查看與該群集關聯的時序。  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 範例結果︰  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 以此識別碼表示的節點包含 "Women's Mountain Shorts" 產品後之時序的清單，以及支援與機率的值。  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 範例結果︰  
  
|t.Product2|t.P2 Support|t.P2 Probability|  
|----------------|------------------|----------------------|  
|Missing|230.7419|0.456012|  
|Classic Vest|8.16129|0.016129|  
|Cycling Cap|60.83871|0.120235|  
|Half-Finger Gloves|30.41935|0.060117|  
|Long-Sleeve Logo Jersey|86.80645|0.171554|  
|Racing Socks|28.93548|0.057185|  
|Short-Sleeve Classic Jersey|60.09677|0.118768|  
  
 請注意，與 Women's Mountain Shorts 相關之各種時序的支援在模型中為 506。 轉換的支援值最多可以增加到 506。 不過，這些數目並不是完整的數目，如果您希望支援只表示包含每個轉換之案例的計數，這似乎有點多。 但是，因為建立群集的方法會計算部分成員資格，群集中任何轉換的機率都必須透過屬於該特定群集的機率加權。  
  
 例如，如果有四個群集，特定時序屬於群集 1 的機會可能有 40%，屬於群集 2 的機會有 30%，屬於群集 3 的機會有 20%，而屬於群集 3 的機會有 10%。 在演算法決定轉換可能所屬的群集之後，會在群集中透過群集優先機率加權機率。  
  
###  <a name="bkmk_Query3"></a>範例查詢3：使用系統預存程式  
 您可以從這些查詢範例中了解，儲存在模型中的資訊相當複雜，而且您可能需要建立多個查詢，才能取得所需的資訊。 不過，Microsoft 時序群集檢視器會提供一組強大的工具，可以用圖形化的方式瀏覽包含在時序群集模型中的資訊，而且您也可以使用檢視器查詢與向下鑽研模型。  
  
 在多數的情況下，呈現在 Microsoft 時序群集檢視器中的資訊是使用 Analysis Services 系統預存程序所建立，用於查詢模型。 您可以根據模型內容撰寫資料採礦延伸模組 (DMX) 查詢來擷取相同的資訊，但是 Analysis Services 系統預存程序會再瀏覽或測試模型時提供一個方便的捷徑。  
  
> [!NOTE]  
>  系統預存程序用於 Microsoft 針對與 Analysis Services 伺服器互動所提供之伺服器與用戶端進行的內部處理。 因此，Microsoft 保留隨時進行變更的權限。 雖然此處所述的系統預存程序是為了提供您的方便，但是我們不支援在生產環境中使用這些預存程序。 為確保生產環境的穩定性與相容性，您應該一律使用 DMX 撰寫您自己的查詢。  
  
 本節提供一些如何使用系統預存程序，根據時序群集模型建立查詢的範例：  
  
#### <a name="cluster-profiles-and-sample-cases"></a>群集設定檔與範例案例  
 [群集設定檔] 索引標籤會顯示模型中的群集清單、每個群集的大小，以及表示包含在群集中之狀態的長條圖。 有兩個系統預存程序可以在查詢中用於擷取類似的資訊：  
  
-   
  `GetClusterProfile` 會傳回叢集的特性，以及在叢集的 NODE_DISTRIBUTION 資料表中找到的所有資訊。  
  
-   
  `GetNodeGraph` 會傳回可用於建構群集之數學圖形表示的節點與邊緣 (對應到您在時序群集檢視的第一個索引標籤上所看到的節點與邊緣)。 這些節點是群集，而邊緣則代表加權或強度。  
  
 下列範例說明如何使用系統預存程序 `GetClusterProfiles`，傳回模型中的所有群集及其個別的設定檔。 這個預存程序會執行一連串的 DMX 陳述式，以傳回模型中的一組完整設定檔。 不過，若要使用此預存程序，您必須知道此模型的位址。  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 下列範例說明如何使用系統預存程序 `GetNodeGraph`，並指定群集識別碼 (通常與群集名稱中的數字相同) 來擷取特定群集 (群集 12) 的設定檔。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 如果您省略群集識別碼，如下列查詢所示， `GetNodeGraph` 則會傳回所有群集設定檔已排序的扁平化清單：  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 
  **[群集設定檔]** 索引標籤也會顯示模型範例案例的長條圖。 這些範例案例代表模型的理想化案例。 這些案例在模型中的儲存方式與定型資料的儲存方式不同，您必須使用特殊的語法才能擷取模型的範例案例。  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 如需詳細資訊，請參閱 [SELECT FROM &#60;model&#62;.SAMPLE_CASES &#40;DMX&#41;](/sql/dmx/select-from-model-dmx)。  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>群集特性與群集辨識  
 
  **[群集特性]** 索引標籤會摘要每個群集的主要屬性，並以機率排序。 您可以找出有多少個案例屬於某個群集，以及群集中的案例分配狀況。每個特性都有特定的支援。 若要查看特定群集的特性，您必須知道該群集的識別碼。  
  
 下列範例使用系統預存程序 `GetClusterCharacteristics`，傳回機率分數超過 0.0005 指定臨界值之群集 12 的所有特性。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 若要傳回所有群集的特性，您可以將群集識別碼留空。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 下列範例會呼叫系統預存程序 `GetClusterDiscrimination` 來比較群集 1 與群集 12 的特性。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 如果您要使用 DMX 撰寫自己的查詢來比較兩個群集，或比較某個群集及其補充，您必須先擷取一組特性，再擷取您感興趣之特定群集的特性，然後比較這兩組特性。 此案例較為複雜，而且通常需要進行某些用戶端處理。  
  
#### <a name="states-and-transitions"></a>狀態與轉換  
 Microsoft 時序群集的 **[狀態轉換]** 索引標籤會在後端執行複雜的查詢，藉以擷取並比較不同群集的統計資料。 若要重新產生這些結果，需要更複雜的查詢並進行某些用戶端處理。  
  
 不過，您可以使用＜ [內容查詢](#bkmk_ContentQueries)＞一節的範例 2 中所述的 DMX 查詢，擷取時序或個別轉換的機率和狀態。  
  
## <a name="using-the-model-to-make-predictions"></a>使用模型進行預測  
 時序群集模型的預測查詢可以使用多個搭配其他群集模型使用的預測函數。 此外，您可以使用特殊的預測函數 [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx)進行建議或預測後續狀態。  
  
###  <a name="bkmk_Query4"></a>範例查詢4：預測下一個狀態或狀態  
 您可以使用 [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx) 函數來預測給定值下一個最可能的狀態。 您也可以預測多個後續狀態：例如，您可以傳回客戶可能購買的前三個產品的清單來顯示建議清單。  
  
 下列範例查詢是單一預測查詢，可傳回前五個預測及其機率。 由於模型中包含巢狀資料表，因此您在進行預測時，必須使用巢狀資料表 `[v Assoc Seq Line Items]`做為資料行參考。 同時，當您提供值做為輸入時，您必須同時加入案例資料表與巢狀資料表資料行，如巢狀 SELECT 陳述式所示。  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 範例結果︰  
  
|Expression.$Sequence|Expression.Line Number|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Cycling Cap|  
|2||Cycling Cap|  
|3||Sport-100|  
|4||Long-Sleeve Logo Jersey|  
|5||Half-Finger Gloves|  
|6||All-Purpose Bike Stand|  
|7||All-Purpose Bike Stand|  
  
 即使您只預期有一個資料行，結果中仍有三個資料行，因為查詢永遠會為案例資料表傳回一個資料行。 此處的結果已扁平化，否則，查詢將會傳回包含兩個巢狀資料表資料行的單一資料行。  
  
 $sequence 資料行是 `PredictSequence` 函數預設傳回的資料行，可排序預測結果。 在模型中比對時序索引鍵時需要 `[Line Number]`資料行，但是不會輸出這些索引鍵。  
  
 有趣的是，All-Purpose Bike Stand 後的前幾個預測時序為 Cycling Cap 和 Cycling Cap。 這不是錯誤。 根據資料呈現給客戶的方式，以及定型模型時的分組方式，很可能有這種時序。 例如，如果沒有辦法指定數量，客戶可能會購買一個 Cycling Cap (紅色)，然後又購買另一個 Cycling Cap (藍色)，或者在一個資料列同時購買兩個。  
  
 資料列 6 和 7 中的值為預留位置。 當您到達可能轉換之鏈結的結尾時，當做輸入傳遞的值會加入到結果中，而非終止預測結果。 例如，如果您將預測的數目增加到 20，資料列 6-20 的值將會相同，也就是 All-Purpose Bike Stand。  
  
## <a name="function-list"></a>函數清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法也支援下表所列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用量|  
|[&#40;DMX&#41;的叢集](/sql/dmx/cluster-dmx)|傳回最可能包含輸入案例的群集|  
|[DMX&#41;的 ClusterDistance &#40;](/sql/dmx/clusterdistance-dmx)|傳回輸入案例與指定之群集的距離；如果沒有指定任何群集，則會傳回輸入案例與最可能之群集的距離。<br /><br /> 此函數可以搭配任何種類的叢集模型 (EM、K-Means 等) 使用，但是結果會隨著演算法而有所不同。|  
|[DMX&#41;的 ClusterProbability &#40;](/sql/dmx/clusterprobability-dmx)|傳回輸入案例屬於指定之群集的機率。|  
|[DMX&#41;的 IsInNode &#40;](/sql/dmx/isinnode-dmx)|指示指定的節點是否包含目前案例。|  
|[DMX&#41;的 PredictAdjustedProbability &#40;](/sql/dmx/predictadjustedprobability-dmx)|傳回指定狀態的已調整機率。|  
|[DMX&#41;的 PredictAssociation &#40;](/sql/dmx/predictassociation-dmx)|預測關聯的成員資格。|  
|[DMX&#41;的 PredictCaseLikelihood &#40;](/sql/dmx/predictcaselikelihood-dmx)|傳回輸入案例符合現有模型的可能性。|  
|[&#40;DMX&#41;的 PredictHistogram](/sql/dmx/predicthistogram-dmx)|傳回表示給定資料行的預測長條圖的資料表。|  
|[DMX&#41;的 PredictNodeId &#40;](/sql/dmx/predictnodeid-dmx)|傳回案例分類之節點的 Node_ID。|  
|[DMX&#41;的 [Predictprobability] &#40;](/sql/dmx/predictprobability-dmx)|傳回指定狀態的機率。|  
|[DMX&#41;的 PredictSequence &#40;](/sql/dmx/predictsequence-dmx)|預測指定之時序資料集合的未來時序值。|  
|[DMX&#41;的 PredictStdev &#40;](/sql/dmx/predictstdev-dmx)|傳回指定之資料行的預測標準差。|  
|[DMX&#41;的 PredictSupport &#40;](/sql/dmx/predictsupport-dmx)|傳回指定狀態的支援值。|  
|[DMX&#41;的 PredictVariance &#40;](/sql/dmx/predictvariance-dmx)|傳回指定之資料行的變異數。|  
  
 如需所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法通用函數的清單，請參閱[一般預測函數 &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)。 如需特定函數的語法，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢](data-mining-queries.md)   
 [Microsoft 時序群集演算法技術參考](microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Microsoft 時序群集演算法](microsoft-sequence-clustering-algorithm.md)   
 [時序群集模型的採礦模型內容 &#40;Analysis Services 資料採礦&#41;](mining-model-content-for-sequence-clustering-models.md)  
  
  
