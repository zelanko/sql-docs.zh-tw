---
title: 決策樹模型的採礦模型內容 (Analysis Services-資料採礦) |Microsoft 文件
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
- mining model content, decision tree models
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
ms.assetid: ac358399-10f8-4238-be32-a914a2e49048
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7ced4dd7c81ab5c3851b180394d75d80d35c502f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033149"
---
# <a name="mining-model-content-for-decision-tree-models-analysis-services---data-mining"></a>Mining Model Content for Decision Tree Models (Analysis Services - Data Mining)
  本主題描述使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法的模型專用的採礦模型內容。 採礦模型內容的所有模型類型的一般說明，請參閱[採礦模型內容&#40;Analysis Services-資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)。 請務必記住，Microsoft 決策樹演算法是一種混合式演算法，可以建立功能非常不同的模型：決策樹可以代表關聯、規則，甚至線性迴歸。 樹狀結構基本上相同，但是您解譯資訊的方式將取決於建立模型的目的。  
  
##  <a name="bkmk_Top"></a> 了解決策樹模型的結構  
 決策樹模型擁有代表模型及其中繼資料的單一父節點。 父節點下為獨立的樹狀結構，代表您選取的可預測屬性。 例如，如果您設定決策樹模型來預測客戶是否會購買某樣東西，而且提供性別和收入的輸入，此模型就會建立購買屬性的單一樹狀結構，其中包含針對性別和收入相關條件分類的許多分支。  
  
 不過，如果您接著要加入個別的可預測屬性來參與顧客獎勵計畫，此演算法將會在父節點下建立兩個個別的樹狀結構。 其中一個樹狀結構包含購買的分析，而另一個樹狀結構則包含顧客獎勵計畫的分析。  如果您使用決策樹演算法來建立關聯模型，此演算法會為每個要進行預測的產品建立一個個別的樹狀結構，而且該樹狀結構會包含可選取之目標屬性的其他所有產品組合。  
  
> [!NOTE]  
>  如果您的模型包含多個樹狀結構，可以在 **[Microsoft 樹狀檢視器]** 中，一次僅檢視一個樹狀結構。 不過，在 **[一般內容樹狀檢視器]** 中，相同模型中的所有樹狀結構會同時顯示出來。  
  
 ![決策樹模型內容結構](../media/modelcontentstructure-dt.gif "的決策樹模型內容結構")  
  
 每個可預測屬性的樹狀結構所包含的資訊會描述您選擇的輸入資料行如何影響該特定可預測屬性和結果。 每個樹狀結構開頭都是一個包含可預測屬性的節點 (NODE_TYPE = 9)，後面接著代表輸入屬性的一連串節點 (NODE_TYPE = 10)。 屬性會對應到案例層級的資料行或巢狀資料表資料行的值，這通常是巢狀資料表之 `Key` 資料行中的值。  
  
 內部和分葉節點代表分岔條件。 樹狀結構可以在相同的屬性上分岔多次。 例如， **TM_DecisionTree** 模型可能會針對 [Yearly Income] 和 [Number of Children] 分割，然後針對樹狀結構下的 [Yearly Income] 再分割一次。  
  
 Microsoft 決策樹演算法也可以在所有或部分樹狀結構中包含線性迴歸。 如果您製作模型的屬性是連續的數值資料類型，此模型可以在屬性之間的關聯性能夠以線性方式製作模型的任何位置，建立迴歸樹狀節點 (NODE_TYPE = 25)。 在此情況下，節點包含迴歸公式。  
  
 不過，如果可預測的屬性擁有離散值，或者如果數值經過儲存或離散化，此模型永遠會建立分類樹狀結構 (NODE_TYPE =2)。 分類樹狀結構針對每個屬性值，可以擁有多個分支或內部樹狀節點 (NODE_TYPE =3)。 不過，不一定要在屬性的每個值上進行分岔。  
  
 Microsoft 決策樹演算法不允許使用連續資料類型當做輸入，因此，如果任何資料行有連續數值資料類型，就會將這些值離散化。 此演算法會在所有連續屬性的分岔點執行自己的離散化。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會自動選擇儲存連續屬性的方法，不過，您可以控制如何將輸入中的連續值離散化，方法是，將採礦結構資料行的內容類型設定為 `Discretized`，然後設定 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 或 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 屬性。  
  
##  <a name="bkmk_ModelContent"></a> 決策樹模型的模型內容  
 本節僅針對採礦模型內容中與決策樹模型具有特定相關的資料行，提供詳細資料和範例。 如需一般用途資料行中的結構描述資料列集和採礦模型術語的說明資訊，請參閱[採礦模型內容&#40;Analysis Services-資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)。  
  
 MODEL_CATALOG  
 模型儲存位置所在資料庫的名稱。  
  
 MODEL_NAME  
 模型的名稱。  
  
 ATTRIBUTE_NAME  
 對應至這個節點之屬性的名稱。  
  
 NODE_NAME  
 永遠與 NODE_UNIQUE_NAME 相同。  
  
 NODE_UNIQUE_NAME  
 節點在模型內的唯一識別項。 這項值不能被改變。  
  
 若是決策樹模型，唯一名稱遵循下列慣例，這個慣例不適用於所有演算法：  
  
 任何特定節點的子節點全部都有相同的十六進位前置詞，後面接著另一個十六進位數字，代表子節點在父系內部的順序。 您可以使用前置詞來推斷路徑。  
  
 NODE_TYPE  
 在決策樹模型中，會建立下列類型的節點：  
  
|節點類型|描述|  
|---------------|-----------------|  
|1 (模型)|模型的根節點。|  
|2 (樹狀結構)|在模型中分類樹狀結構的父節點。 標示為 **「All」**。|  
|3 (內部)|內部分支的標頭，可在分類樹狀結構或迴歸樹狀結構中找到。|  
|4 (分佈)|分葉節點，可在分類樹狀結構或迴歸樹狀結構中找到。|  
|25 (迴歸樹狀結構)|在模型內迴歸樹狀結構的父節點。 標示為 **「All」**。|  
  
 NODE_CAPTION  
 提供顯示用途的好記名稱。  
  
 在建立模型時，NODE_UNIQUE_NAME 的值會自動用來當做標題。 不過，您可以用程式設計的方式或使用檢視器來變更 NODE_CAPTION 的值，以更新群集的顯示名稱。 標題會透過模型自動產生。 標題的內容取決於模型的類型以及節點類型。  
  
 在決策樹模型中，NODE_CAPTION 和 NODE_DESCRIPTION 的資訊不同，端視樹狀結構中的層級而定。 如需詳細資訊與範例，請參閱 [節點標題與節點描述](#NodeCaption)。  
  
 CHILDREN_CARDINALITY  
 節點所擁有子系數目的估計。  
  
 **父節點** ：指出已製作模型之可預測屬性的數目。 每個可預測的屬性都會建立一個樹狀結構。  
  
 **樹狀節點** ：每個樹狀結構的 **All** 節點都會告訴您目標屬性使用多少個值。  
  
-   如果目標屬性是離散的，該值等於 `Missing` 狀態的相異值數目加 1。  
  
-   如果可預測的屬性是連續的，此值會告訴您有多少值區用於製作連續屬性的模型。  
  
 **分葉節點** ：永遠為 0。  
  
 PARENT_UNIQUE_NAME  
 節點之父系的唯一名稱。 任何根層級的節點都會傳回 NULL。  
  
 NODE_DESCRIPTION  
 節點的描述。  
  
 在決策樹模型中，NODE_CAPTION 和 NODE_DESCRIPTION 的資訊不同，端視樹狀結構中的層級而定。  
  
 如需詳細資訊與範例，請參閱 [節點標題與節點描述](#NodeCaption)。  
  
 NODE_RULE  
 規則的 XML 描述，其中描述來自直屬父節點之目前節點的路徑。  
  
 如需詳細資訊與範例，請參閱 [節點規則與臨界規則](#NodeRule)。  
  
 MARGINAL_RULE  
 規則的 XML 描述，其中描述從模型父節點到目前節點的路徑。  
  
 如需詳細資訊，請參閱 [節點規則與臨界規則](#NodeRule)。  
  
 NODE_PROBABILITY  
 與此節點關聯的機率。  
  
 如需詳細資訊，請參閱 [機率](#bkmk_NodeDist_Discrete)。  
  
 MARGINAL_PROBABILITY  
 從父節點到達節點的機率。  
  
 如需詳細資訊，請參閱 [機率](#bkmk_NodeDist_Discrete)。  
  
 NODE_DISTRIBUTION  
 包含節點之機率長條圖的資料表。 此資料表中的資訊會隨著可預測屬性為連續或離散變數而有所不同。  
  
 **模型根節點** ：此資料表是空的。  
  
 **(All) 節點** ：包含完整模型的摘要。  
  
 **內部節點** ：包含其分葉節點的彙總統計資料。  
  
 **分葉節點** ：假設路徑中的所有條件都引導至目前的分葉節點，則包含預測結果的支援與機率。  
  
 **迴歸節點** ：包含代表輸入和可預測屬性間關聯性的迴歸公式。  
  
 如需詳細資訊，請參閱＜ [離散屬性的節點分佈](#bkmk_NodeDist_Discrete) ＞和＜ [連續屬性的節點分佈](#bkmk_RegressionNodes)＞。  
  
 NODE_SUPPORT  
 支援這個節點的案例數目。  
  
 MSOLAP_MODEL_COLUMN  
 指出包含可預測屬性的資料行。  
  
 MSOLAP_NODE_SCORE  
 顯示與節點相關聯的分數。 如需詳細資訊，請參閱 [節點分數](#NodeScore)。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 主要用於顯示用途。  
  
## <a name="remarks"></a>備註  
 不像在貝式機率分類或類神經網路模型中找到的臨界統計資料節點，決策樹模型沒有儲存整個模型之統計資料的個別節點。 但是此模型會針對每個可預測的屬性建立一個個別的樹狀結構，且 (All) 節點位於樹狀結構的頂端。 樹狀結構彼此之間無關。 如果您的模型只包含一個可預測的屬性，則只有一個樹狀結構，因此只有一個 (All) 節點。  
  
 代表輸出屬性的每個樹狀結構都會另外細分為代表分岔的內部分支 (NODE_TYPE = 3)。 每個樹狀結構都包含關於目標屬性分佈的統計資料。 此外，每個分葉節點 (NODE_TYPE = 4) 都包含描述輸入屬性及其值的統計資料，以及支援每個屬性和值配對之案例的數目。 因此，在決策樹的任何分支中，您可以輕鬆檢視資料的機率或分佈，而不必查詢來源資料。 樹狀結構的每個層級都必須代表其直屬子節點的總和。  
  
 如需如何擷取這些統計資料的範例，請參閱[決策樹模型查詢範例](decision-trees-model-query-examples.md)。  
  
## <a name="example-of-decision-tree-structure"></a>決策樹結構的範例  
 若要了解決策樹如何運作，請考慮使用範例，例如，AdventureWorks 自行車購買者案例。 假設可預測的屬性為客戶購買的項目，決策樹演算法會嘗試在您提供的所有輸入中找出資料的一個資料行，可以用最有效的方式偵測到可能會購買自行車的客戶，以及可能不會購買自行車的客戶。 例如，此模型可能會發現「年齡」是購買行為的最佳指標。 特別是，超過 30 歲的客戶很可能購買自行車，而其他所有客戶則可能不會購買。 在這個案例中，此模型會在 [Age] 屬性上建立一個 *「分岔」* (Split)。 也就是說，樹狀結構分成兩個分支，其中一個分支包含超過 30 歲的客戶，另一個分支則包含 30 歲以下的客戶。 在模型結構中，新的分支會以兩個新的內部樹狀結構 (NODE_TYPE = 3) 代表。  
  
 此模型會針對每個分支，繼續尋找用於區分客戶的其他屬性。 如果資料中的證據不足，無法繼續建立客戶的子群組，此模型會停止建立樹狀結構。 此模型也會在節點中的案例數太小而無法繼續時，停止建立樹狀結構，而不管分岔是否妥當，或者值為 Null 或遺漏。 早期停止樹狀結構的成長，您就可以防止模型與特定一組資料的定型太接近。  
  
 每個內部樹狀節點都包含分葉節點，可提供給定目前分類結果的細分結果。 例如，您可能有一個代表 Age >= 30，而且 Gender = Male 的內部節點。 此群組的節點會顯示此類別中購買的客戶數目，或者未購買的客戶數目。 例如，分類可能包含下列樹狀結構分岔：  
  
|內部樹狀結構|「分岔」|  
|-------------------|-----------|  
|Age >= 30|Age >= 30 而且 Gender = Male|  
||Age >= 30 而且 Gender = Female|  
|Age < 30|Age < 30 而且 Gender = Male|  
||年齡\<30 而且 Gender = Female|  
  
 當您使用決策樹模型進行預測時，此模型會採用您所提供的屬性當做引數，然後遵照屬性的路徑向下到樹狀結構。 一般而言，所有預測都會到分葉，而內部節點則僅用於分類。  
  
 分葉節點的 NODE_TYPE 永遠都為 4 (分佈)，而且包含的長條圖會根據您提供的屬性，顯示每個結果的機率 (購買或不購買)。 例如，如果您要求預測超過 60 歲的男性新客戶，此模型將會查詢對應的節點 (Age > 30 而且 Gender = Male)，然後傳回您指定之結果的機率。 這些機率儲存在節點的 [NODE_DISTRIBUTION](#bkmk_NodeDist_Discrete) 資料表中。  
  
 如果可預測的屬性是連續數字，此演算法會嘗試建立迴歸公式，以製作可預測屬性和輸入之間關聯性的模型。  
  
###  <a name="NodeCaption"></a> 節點標題與節點描述  
 在決策樹模型中，節點標題與節點描述包含類似的資訊。 不過，節點描述更為完整，而且在您向分葉節點移得更近時，會包含更多資訊。 節點標題與節點描述都是當地語系化的字串。  
  
|||  
|-|-|  
|**NODE_CAPTION**|顯示區別相對於父節點之該特定節點的屬性。 節點標題會定義以母體為基礎之分岔條件的子區段。 例如，如果分岔位於 [Age]，和它三向分岔，三個子節點可能的節點標題"[Age] < 40"、"40 < = [Age] \< 50"、"[Age] > = 50"。|  
|**NODE_DESCRIPTION**|包含區別各節點之屬性的完整清單，從模型父節點開始。 例如，Product name = Apple 而且 Color = Red。|  
  
###  <a name="NodeRule"></a> 節點規則與臨界規則  
 NODE_RULE 和 MARGINAL_RULE 資料行包含與 NODE_CAPTION 和 NODE_DESCRIPTION 資料行相同的資訊，但是將資訊表示為 XML 片段。 節點規則為 XML 版本的完整路徑，而臨界規則會指出最近的分岔。  
  
 以 XML 片段表示的屬性可以很簡單，也可以很複雜。 簡單的屬性包含模型資料行的名稱以及屬性的值。 如果模型資料行包含巢狀資料表，巢狀資料表屬性會以資料表名稱、索引鍵值和屬性的串連表示。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援 2.0 版的 PMML 標準，其擴充模組支援巢狀資料表的使用。 如果您的資料包含巢狀資料表，而且您要產生 PMML 版本的模型，模型中包含預測的所有元素都會標示為闊重模組。  
  
###  <a name="bkmk_NodeDist_Discrete"></a> 離散屬性的節點分佈  
 在決策樹模型中，NODE_DISTRIBUTION 資料表包含實用的統計資料。 不過，統計資料的類型取決於樹狀結構預測離散屬性還是連續屬性。 本節描述離散屬性之節點分佈統計資料的意義。  
  
#### <a name="attribute-name-and-attribute-value"></a>屬性名稱與屬性值  
 在分類樹狀結構中，屬性名稱永遠包含可預測資料行的名稱。 這個值會告訴您樹狀結構預測的項目。 由於單一樹狀結構永遠代表單一可預測的屬性，因此這個值在樹狀結構中會重複出現。  
  
 若是離散資料類型，屬性值欄位會列出可預測資料行的可能值，加上 `Missing` 值。  
  
#### <a name="support"></a>支援  
 每個節點的支援值都會告訴提此節點包含多少案例。 您應該在 (All) 層級看到用於定型模型之案例的完整計數。 對於樹狀結構中的每個分岔，支援值是分組到樹狀結構該節點之案例的計數。 分葉節點中的案例總和務必等於樹狀結構父節點中的案例計數。  
  
 對於代表連續屬性的節點，資料中出現的 Null 可能會導致某些反直覺式結果。 例如，如果有 m 個案例，平均值會計算為 sum(all cases)/n，其中 n 是小於 m 的數字，而 m-n 表示遺漏值之案例的計數。 支援也會以 n 表示。  
  
#### <a name="probability"></a>機率  
 與每個節點關聯的機率會告訴您整個資料集中所有案例都會在此特定節點結束的機率。 機率分數會同時針對整個樹狀結構和直屬分岔計算。  
  
 例如，下列資料表顯示非常簡單的模型，其中包含 100 個案例。  
  
|內部樹狀結構|案例|分葉節點|案例|相對於父節點的機率|相對於最上層節點的機率|  
|-------------------|-----------|---------------|-----------|-----------------------------------------|--------------------------------------|  
|Age >= 30|60|Age >= 30 而且 Gender = Male|50|50/60 = .83|50/100 = .5|  
|||Age >= 30 而且 Gender = Female|10|10/60 = .16|10/100 = .10|  
|Age < 30|40|Age < 30 而且 Gender = Male|30|30/40 = .75|30/100 = .30|  
|||Age < 30 而且 Gender = Female|10|10/40 = .25|10/100 = .10|  
  
 在所有模型中進行小調整就可以計算可能的遺漏值。 若是連續屬性，每個值範圍以狀態表示 (例如，Age \<30、 Age = 30，和 Age > 30) 和機率計算方式如下： 狀態存在 (值 = 1)，其他特定狀態存在 (值 = 0)，狀態是`Missing`. 如需如何調整機率來表示遺漏值的詳細資訊，請參閱[遺漏值 &#40;Analysis Services - 資料採礦&#41;](missing-values-analysis-services-data-mining.md)。  
  
 每個節點的機率幾乎都直接從分佈計算，如下所示：  
  
 機率 = (狀態的支援 + 先前狀態的支援) / (節點支援加上先前節點支援)  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用每個節點的機率比較已儲存的機率與先前的機率來判斷父節點到子節點的路徑是否表示堅定的推斷。  
  
 進行預測時，分佈的機率必須與節點的機率對稱，使機率平穩。 例如，如果樹狀結構中的分岔以 9000/1000 的比例分隔案例，該樹狀結構就非常不對稱。 因此，來自小分支的預測加權不應該與來自包含多個案例之分支的預測加權相同。  
  
#### <a name="variance"></a>Variance  
 「變異數」是在給定預期分佈的情況下，值如何在範例中散佈的量值。 若是離散值，定義的變異數為 0。  
  
 如需如何計算連續值之變異數的資訊，請參閱[線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
#### <a name="value-type"></a>值類型  
 值類型資料行會提供 NODE_DISTRIBUTION 資料表中的其他資料行所提供之數值意義的相關資訊。 您可以使用查詢中的值類型，從巢狀資料表擷取特定的資料列。 如需範例，請參閱[決策樹模型查詢範例](decision-trees-model-query-examples.md)。  
  
 在 <xref:Microsoft.AnalysisServices.AdomdClient.MiningValueType> 列舉的類型中，下列類型用於分類樹狀結構。  
  
|值類型|描述|  
|----------------|-----------------|  
|1 (遺漏)|指出與遺漏值相關的計數、機率或其他統計資料。|  
|4 (離散)|指出與離散或離散化值相關的計數、機率或其他統計資料。|  
  
 如果模型包含連續的可預測屬性，樹狀結構可能也包含對迴歸公式而言唯一的值類型。 如需用於迴歸樹狀結構之實值型別的清單，請參閱[線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
###  <a name="NodeScore"></a> 節點分數  
 節點分數代表樹狀結構每個層級上稍微不同的資訊。 一般而言，此分數是一個數值，可告訴您條件式分割所達成的分岔效果。 此值會以雙線表示，其中的值越大越好。  
  
 根據定義，模型節點與所有分葉節點的節點分數都為 0。  
  
 若是代表每個樹狀結構最上層的 (All) 節點，MSOLAP_NODE_SCORE 資料行會在整個樹狀結構中包含最佳的分岔準則。  
  
 若是樹狀結構中的其他所有節點 (分葉節點除外)，每個節點的分數都代表目前節點的最佳分岔準則，減去父節點的分岔準則。 父節點的分岔準則通常永遠比任何其中一個子節點的分岔準則好。 那是因為理論上決策樹模型會先針對最重要的屬性分岔。  
  
 計算分岔準則的方式有很多，端視您選擇的演算法參數而定。 如何針對每個計分方法計算分數不在本主題的討論範圍內。 如需詳細資訊，請參閱[參考資料網站上的＜](http://go.microsoft.com/fwlink/?LinkId=45963)了解 Bayesian 網路：知識與統計資料的組合 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ＞。  
  
> [!NOTE]  
>  如果您建立的決策樹模型同時擁有連續和離散的可預測屬性，您將會在 (All) 節點中看到代表每個樹狀結構類型完全不同的分數。 每個模型都應該分別考量，而且用於計分迴歸的方法與用於計分分類的方法完全不同。 節點分數值無法進行比較。  
  
##  <a name="bkmk_RegressionNodes"></a> 決策樹模型中的迴歸節點  
 如果決策樹模型包含可預測的屬性與連續的數值資料，Microsoft 決策樹演算法會嘗試在資料中，找出已預測狀態與輸入變數間關聯性為線性的區域。 如果演算法成功找出線性關聯性，該演算法就會建立一個代表線性迴歸的特殊樹狀結構 (NODE_TYPE = 25)。 這些迴歸樹狀節點比代表離散值的節點更為複雜。  
  
 一般而言，迴歸會將連續相依 (可預測的變數) 中的變更對應為輸入中變更的功能。 如果相依變數有任何連續輸入，而且輸入和已預測值之間的關聯性夠穩定，可以當做線條圖計算，迴歸的節點就會包含公式。  
  
 不過，如果輸入和已預測值之間的關聯性為 *「非線性的」*(Nonlinear)，就會建立分岔，如同標準決策樹一樣。 例如，假設 A 是可預測的屬性，而 B 和 C 是輸入，其中 C 是連續的值類型。 如果 A 和 C 之間的關聯性在部分資料中相當穩定，但在部分資料中並不穩定，此演算法將會建立分岔來表示不同的資料區域。  
  
|分岔條件|節點的結果|  
|---------------------|--------------------|  
|如果 n \< 5|關聯性可以表示為方程式 1|  
|如果 n 介於 5 和 10 之間|無方程式|  
|如果 n > 10|關聯性可以表示為方程式 2|  
  
 如需迴歸節點的詳細資訊，請參閱[線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型內容&#40;Analysis Services-資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)   
 [資料採礦模型檢視器](data-mining-model-viewers.md)   
 [資料採礦查詢](data-mining-queries.md)   
 [Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)  
  
  