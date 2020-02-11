---
title: 群集模型查詢範例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- content queries [DMX]
- clustering algorithms [Analysis Services]
ms.assetid: bf2ba332-9bc6-411a-a3af-b919c52432c8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4996ba378319e442df07a4ff09af3404034474d9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085723"
---
# <a name="clustering-model-query-examples"></a>叢集模型查詢範例
  當您根據資料採礦模型建立查詢時，可以擷取有關模型的中繼資料或建立內容查詢，以提供有關在分析中所發現之模式的詳細資料。 或者，您可以建立預測查詢，這會使用模型中的模式對新資料進行預測。 每種查詢都會提供不同的資訊。 例如，內容查詢可能會提供有關所找到群集的詳細資料，預測查詢則會告訴您最可能包含新資料點的群集。  
  
 本節說明如何針對以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 叢集演算法為基礎的模型建立查詢。  
  
 **內容查詢**  
  
 [使用 DMX 取得模型中繼資料](#bkmk_Query1)  
  
 [從架構資料列集抓取模型中繼資料](#bkmk_Query2)  
  
 [傳回叢集或群集清單](#bkmk_Query3)  
  
 [傳回叢集的屬性](#bkmk_Query4)  
  
 [使用系統預存程式傳回叢集設定檔](#bkmk_Query5)  
  
 [尋找叢集的群集辨識因素](#bkmk_Query6)  
  
 [傳回屬於群集的案例](#bkmk_Query7)  
  
 **預測查詢**  
  
 [從群集模型預測結果](#bkmk_Query8)  
  
 [判斷叢集成員資格](#bkmk_Query9)  
  
 [以機率和距離傳回所有可能的群集](#bkmk_Query10)  
  
##  <a name="bkmk_top2"></a>尋找有關模型的資訊  
 所有的採礦模型都會公開演算法根據標準化結構描述所學習的內容，也就是採礦模型結構描述資料列集。 您可以藉由使用資料採礦延伸模組 (DMX) 陳述式來針對採礦模型結構描述資料列集建立查詢。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您也可以將結構描述資料列集當做系統資料表直接進行查詢。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query1"></a>範例查詢1：使用 DMX 取得模型中繼資料  
 下列查詢會傳回有關您在「基本資料採礦教學課程」中所建立的叢集模型 `TM_Clustering`的基本中繼資料。 叢集模型的父節點所提供的中繼資料包含模型的名稱、模型儲存位置所在的資料庫，以及模型中子節點的數目。 此查詢會使用 DMX 內容查詢從模型的父節點擷取中繼資料：  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  您必須將資料行 CHILDREN_CARDINALITY 的名稱包含在括號中，好與相同名稱的「多維度運算式」(MDX) 保留關鍵字加以區別。  
  
 範例結果︰  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|叢集模型|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|全部|  
  
 如需這些資料行在叢集模型中代表意義的定義，請參閱[叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-clustering-models-analysis-services-data-mining.md)。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a>範例查詢2：從架構資料列集抓取模型中繼資料  
 藉由查詢資料採礦結構描述資料列集，您可以找到與 DMX 內容查詢所傳回的相同的資訊。 不過，結構描述資料列集會提供某些額外的資料行。 其中包括在建立模型時所使用的參數、上次處理模型的日期和時間，以及模型的擁有者。  
  
 下列範例會傳回建立、修改以及上次處理模型的日期，也會傳回用來建立模型的叢集參數以及培訓集的大小。 這些資訊對於記錄模型或者判斷用來建立現有模型時所使用的群集選項很有用。  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 範例結果︰  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 下午|  
|LAST_PROCESSED|10/12/2007 8:09:54 下午|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT=10,<br /><br /> CLUSTER_SEED=0,<br /><br /> CLUSTERING_METHOD=1,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100,<br /><br /> MINIMUM_SUPPORT=1,<br /><br /> MODELLING_CARDINALITY=10,<br /><br /> SAMPLE_SIZE=50000,<br /><br /> STOPPING_TOLERANCE=10|  
  
 [回到頁首](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>尋找有關群集的資訊  
 叢集模型上最有用的內容查詢所傳回的資訊類型，通常與可以使用 [叢集檢視器]**** 瀏覽的資訊類型相同。 這包括群集設定檔、群集特性和群集辨識。 本章節提供會擷取這些資訊的查詢範例。  
  
###  <a name="bkmk_Query3"></a>範例查詢3：傳回叢集或群集清單  
 因為所有的群集都具有節點類型 5，所以您可以僅針對該類型的節點查詢模型內容，以輕鬆地擷取群集清單。 您也可以篩選由機率或支援所傳回的節點，如下列範例所示。  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 範例結果︰  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|群集 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree , 32 <=Age <=48 , Number Cars Owned=0 , 35964.0771121808 <=Yearly Income <=97407.7163393957 , English Occupation=Professional , Commute Distance=2-5 Miles , Region=North America , Bike Buyer=1 , Number Children At Home=0 , Number Cars Owned=1 , Commute Distance=0-1 Miles , English Education=Bachelors , Total Children=1 , Number Children At Home=2 , English Occupation=Skilled Manual , Marital Status=S , Total Children=0 , House Owner Flag=0 , Gender=F , Total Children=2 , Region=Pacific|  
  
 您可在資料採礦結構描述資料列集中的兩個資料行中找到定義群集的屬性。  
  
-   NODE_DESCRIPTION 資料行包含以逗號分隔的屬性清單。 請注意屬性清單可以針對顯示用途而進行縮寫。  
  
-   NODE_DISTRIBUTION 資料行中的巢狀資料表包含群集的完整屬性清單。 如果用戶端不支援階層式資料列集，則您可以在 SELECT 資料行清單之前加入 FLATTENED 關鍵字傳回巢狀資料表。 如需 FLATTENED 關鍵字使用的詳細資訊，請參閱 [SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](/sql/dmx/select-from-model-dimension-content-dmx)。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query4"></a>範例查詢4：傳回叢集的屬性  
 對於每個叢集而言，[叢集檢視器]**** 會顯示列出屬性及其值的設定檔。 檢視器也會顯示長條圖，以顯示模型中整個案例母體的值分佈情形。 如果是在檢視器中瀏覽模型，則您可以輕鬆地從「採礦圖例」複製長條圖，然後將它貼入至 Excel 或 Word 文件。 也可以使用檢視器的 [群集特性] 窗格，以圖形方式比較不同群集的屬性。  
  
 不過，如果一次必須取得一個以上群集的值，對模型進行查詢是比較簡單的方式。 例如，您在瀏覽模型時，可能會注意到最上面兩個叢集在 `Number Cars Owned`屬性方面不同。 因此可能會想針對每個群集擷取值。  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 程式碼的第一行指定您只想要最上面兩個群集。  
  
> [!NOTE]  
>  依預設，群集會依支援來排序。 因此，NODE_SUPPORT 資料行可以省略。  
  
 程式碼的第二行會加入子 SELECT 陳述式，此陳述式僅會從巢狀資料表資料行傳回特定的資料行； 此外，它也會將巢狀資料表的資料列限制為與目標屬性 `Number Cars Owned`相關的資料列。 為了檢視顯示，巢狀資料表會使用別名。  
  
> [!NOTE]  
>  巢狀資料表資料行 `PROBABILITY`必須包含在括號中，因為它也是 MDX 保留關鍵字的名稱。  
>   
>  範例結果︰  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Missing|0|  
|002|0|0.576980023|  
|002|1|0.406623939|  
|002|2|0.016380082|  
|002|3|1.60E-05|  
|002|4|0|  
|002|Missing|0|  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a>範例查詢5：使用系統預存程式傳回群集設定檔  
 如果不想要使用 DMX 撰寫自己的查詢，也可以呼叫 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 用來使用叢集的系統預存程序當做捷徑。 下列範例將說明如何使用內部預存程序為識別碼 002 的群集傳回設定檔。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 同樣地，您可以使用系統預存程序來傳回特定群集的特性，如下列範例所示：  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 範例結果︰  
  
|屬性|值|頻率|支援|  
|----------------|------------|---------------|-------------|  
|Number Children At Home|0|0.999999829076798|899|  
|區域|北美洲|0.999852875241508|899|  
|Total Children|0|0.993860958572323|893|  
  
> [!NOTE]  
>  資料採礦系統預存程序供內部使用， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 保留依需求變更這些程序的權利。 在實際執行環境中，建議您使用 DMX、AMO 或 XMLA 建立查詢。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query6"></a>範例查詢6：尋找叢集的群集辨識因素  
 [叢集檢視器]**** 的 [叢集辨識]**** 索引標籤可讓您輕鬆地將某個叢集與另一個叢集相比較，或將某個叢集與所有其餘案例 (叢集的補充) 相比較。  
  
 不過，要建立傳回此資訊的查詢可能很複雜，而且您可能需要在用戶端上進行一些額外的處理，並比較兩個或更多查詢的結果。 所以可以使用系統預存程序當做捷徑。  
  
 下列查詢會傳回單一資料表，指出擁有節點識別碼 009 和 007 的兩個群集間的主要辨識因數。 具有正值的屬性會使用群集 009，具有負值的屬性則使用群集 007。  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 範例結果︰  
  
|屬性|值|Score|  
|----------------|------------|-----------|  
|區域|北美洲|100|  
|English Occupation|Skilled Manual|94.9003803898654|  
|區域|歐洲|-72.5041051379789|  
|English Occupation|手動|-69.6503163202722|  
  
 這與您從第一個下拉式清單選取叢集 9 和從第二個下拉式清單選取叢集 7 時，在 [叢集辨識]**** 檢視器的圖表中所展示的資訊相同。 若要將群集 9 與其補充相較，可以使用第二個參數中的空字串，如下列範例所示：  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  資料採礦系統預存程序供內部使用， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 保留依需求變更這些程序的權利。 在實際執行環境中，建議您使用 DMX、AMO 或 XMLA 建立查詢。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a>範例查詢7：傳回屬於群集的案例  
 如果您已在採礦模型上啟用鑽研，則可以建立查詢以傳回有關在模型中所使用案例的詳細資訊。 此外，如果已在採礦結構上啟用鑽研，則您可以使用 [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx) 函數來包含來自基礎結構的資料行。  
  
 下列範例會傳回模型中使用的兩個資料行：Age 和 Region，以及另一個未用於模型中的資料行 First Name。 該查詢只會傳回分類為 Cluster 1 的案例。  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 若要傳回屬於群集的案例，您必須知道群集的識別碼。 您可以在其中一個檢視器中瀏覽模型，以取得群集的識別碼， 或者也可以將群集重新命名以方便參考，在這之後您可以使用名稱來取代識別碼。 不過，您必須知道指派給群集的名稱會在重新處理模型之後遺失。  
  
 [回到頁首](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>使用模型進行預測  
 雖然叢集通常是用來描述和了解資料， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 實作也可以讓您進行有關叢集成員資格的預測，並傳回與預測相關聯的機率。 本章節也針對如何在叢集模型上建立預測查詢提供範例。 您可以藉由指定表格式資料來源對多個案例進行預測，或者也可以藉由建立單一查詢，一次提供一個新值。 為了清楚起見，本節中的範例全都是單一查詢。  
  
 如需如何使用 DMX 建立預測查詢的詳細資訊，請參閱[資料採礦查詢介面](data-mining-query-tools.md)。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query8"></a>範例查詢8：從群集模型預測結果  
 如果您建立的叢集模型包含可預測屬性，則您可以使用模型來建立有關結果的預測。 不過，模型會根據可預測資料行是設定為 `Predict` 或 `PredictOnly`，以不同的方式處理可預測屬性。 如果將資料行的用法設定為 `Predict`，則該屬性的值會加入至群集模型，並在完成的模型中顯示為屬性。 不過，如果將資料行的使用方式設定為 `PredictOnly`，則值不會用來建立群集。 反而是在模式完成後，群集演算法會根據每個案例所屬的群集，為 `PredictOnly` 屬性建立新的值。  
  
 下列查詢會為模型提供單一的新案例，其中與案例有關的唯一資訊是年齡和性別。 SELECT 陳述式指定您有興趣的可預測屬性/值配對，而 [PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx) 函數則告訴您具有這些屬性的案例擁有目標結果的機率。  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 當使用方式設定為 `Predict` 時的結果範例：  
  
|Bike Buyer|運算是|  
|----------------|----------------|  
|1|0.592924735740338|  
  
 當使用方式設定為 `PredictOnly` 並重新處理模型時的結果範例：  
  
|Bike Buyer|運算是|  
|----------------|----------------|  
|1|0.55843544003102|  
  
 在此範例中，模型中的差異並不大。 不過，有時候偵測值的實際散發和模型所預測的情況之間的差異可能很重要。 
  [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) 函數在此案例中很有用，因為它會告訴您在模型已知時的案例可能性。  
  
 PredictCaseLikelihood 函數傳回的數字是機率，因此一定會介於 0 和 1 之間，.5 的值則代表隨機結果。 因此，小於 .5 的分數代表預測的案例在模型已知時不太可能發生，而超過 .5 的分數則代表預測的案例較符合模型的預測。  
  
 例如，下列查詢會傳回兩個代表新範例案例可能性的值。 非正規化的值代表在目前模型已知時的機率。 當您使用 NORMALIZED 關鍵字時，由函數傳回的可能性分數會藉由將「使用模型的機率」除以「不使用模型的機率」來進行調整。  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 範例結果︰  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5.56438372679893E-11|8.65459953145182E-68|  
  
 請注意，這些結果中的數字會以科學記號標記法表示。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query9"></a>範例查詢9：判斷群集成員資格  
 此範例會使用 [叢集 &#40;DMX&#41;](/sql/dmx/cluster-dmx) 函數來傳回最可能包含新案例的叢集，並使用 [ClusterProbability &#40;DMX&#41;](/sql/dmx/clusterprobability-dmx) 函數來傳回該叢集中的成員資格機率。  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 範例結果︰  
  
|$CLUSTER|運算是|  
|--------------|----------------|  
|群集 2|0.397918596951617|  
  
 **注意**根據預設， `ClusterProbability`函數會傳回最可能叢集的機率。 不過，您可以使用 `ClusterProbability('cluster name')`語法來指定不同的叢集。 如果要這麼做，請注意每個預測函數的結果都與其他結果無關。 因此，第二個資料行中的機率分數所參考的群集可以與命名於第一個資料行中的群集不同。  
  
 [回到頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query10"></a>範例查詢10：使用機率和距離傳回所有可能的群集  
 在以上範例中，機率分數並不很高。 若要判斷是否有更好的叢集，可以使用 [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx) 函數搭配 [叢集 &#40;DMX&#41;](/sql/dmx/cluster-dmx) 函數來傳回包含所有可能叢集的巢狀資料表，並附上新案例屬於每個叢集的機率。 FLATTENED 關鍵字可用來將階層式資料列集變更為二維資料表以方便檢視。  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|群集 2|0.602081403048383|0.397918596951617|  
|叢集 10|0.719691686785675|0.280308313214325|  
|叢集 4|0.867772590378791|0.132227409621209|  
|叢集 5|0.931039872200985|0.0689601277990149|  
|叢集 3|0.942359230072167|0.0576407699278328|  
|叢集 6|0.958973668972756|0.0410263310272437|  
|叢集 7|0.979081275926724|0.0209187240732763|  
|叢集 1|0.999169044818624|0.000830955181376364|  
|叢集 9|0.999831227795894|0.000168772204105754|  
|叢集 8|1|0|  
  
 根據預設值，結果是依機率排序。 結果會告訴您，即使 Cluster 2 的機率相當低，Cluster 2 仍是新資料點的最適合項目。  
  
 **注意**額外的資料行`$DISTANCE`代表從資料點到叢集的距離。 根據預設， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法會使用可擴充的 EM 叢集，這種方法會將多個叢集指派給每個資料點，並排列可能叢集的次序。  不過，如果使用 K-means 演算法建立叢集模型，則只能將一個群集指派給每個資料點，且此查詢只會傳回一個資料列。 了解這些差異對於解譯 [PredictCaseLikelihood &#40;DMX&#41;](/sql/dmx/predictcaselikelihood-dmx) 函數來包含來自基礎結構的資料行。 如需 EM 和 K-means 叢集之間差異的詳細資訊，請參閱 [Microsoft 群集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)。  
  
 [回到頁首](#bkmk_top2)  
  
## <a name="function-list"></a>函數清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過，使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 叢集演算法建立的模型支援下表中列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用量|  
|[&#40;DMX&#41;的叢集](/sql/dmx/cluster-dmx)|傳回最可能包含輸入案例的群集。|  
|[DMX&#41;的 ClusterDistance &#40;](/sql/dmx/clusterdistance-dmx)|傳回輸入案例與指定之群集的距離；如果沒有指定任何群集，則會傳回輸入案例與最可能之群集的距離。<br /><br /> 傳回輸入案例屬於指定之群集的機率。|  
|[DMX&#41;的 ClusterProbability &#40;](/sql/dmx/clusterprobability-dmx)|傳回輸入案例屬於指定之群集的機率。|  
|[DMX&#41;的 IsDescendant &#40;](/sql/dmx/isdescendant-dmx)|確定某個節點是否為模型中另一個節點的子系。|  
|[DMX&#41;的 IsInNode &#40;](/sql/dmx/isinnode-dmx)|指示指定的節點是否包含目前案例。|  
|[DMX&#41;的 PredictAdjustedProbability &#40;](/sql/dmx/predictadjustedprobability-dmx)|傳回加權機率。|  
|[DMX&#41;的 PredictAssociation &#40;](/sql/dmx/predictassociation-dmx)|預測關聯資料集的成員資格。|  
|[DMX&#41;的 PredictCaseLikelihood &#40;](/sql/dmx/predictcaselikelihood-dmx)|傳回輸入案例符合現有模型的可能性。|  
|[&#40;DMX&#41;的 PredictHistogram](/sql/dmx/predicthistogram-dmx)|傳回與目前預測值相關之值的資料表。|  
|[DMX&#41;的 PredictNodeId &#40;](/sql/dmx/predictnodeid-dmx)|傳回每個案例的 Node_ID。|  
|[DMX&#41;的 [Predictprobability] &#40;](/sql/dmx/predictprobability-dmx)|傳回預測值的機率。|  
|[DMX&#41;的 PredictStdev &#40;](/sql/dmx/predictstdev-dmx)|傳回指定之資料行的預測標準差。|  
|[DMX&#41;的 PredictSupport &#40;](/sql/dmx/predictsupport-dmx)|傳回指定狀態的支援值。|  
|[DMX&#41;的 PredictVariance &#40;](/sql/dmx/predictvariance-dmx)|傳回指定之資料行的變異數。|  
  
 如需特定函數的語法，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢](data-mining-queries.md)   
 [Microsoft 群集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)   
 [Microsoft 群集演算法](microsoft-clustering-algorithm.md)  
  
  
