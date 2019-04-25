---
title: 採礦模型內容 (Analysis Services-資料採礦) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5fe10a98910f54e4317d0191753d40b9b6b0b94f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62736079"
---
# <a name="mining-model-content-analysis-services---data-mining"></a>Mining Model Content (Analysis Services - Data Mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  當您已經使用基礎採礦結構中的資料來設計及處理採礦模型之後，該採礦模型會是完整的，並包含 *「採礦模型內容」*(Mining Model Content)。 您可以使用此內容來進行預測或分析資料。  
  
 採礦模型內容包含有關模型的中繼資料、有關資料的統計資料及採礦演算法所找到的模式。 根據所使用的演算法而定，模型內容可能會包含迴歸公式、規則和項目集的定義，或是加權和其他統計資料。  
  
 不論所使用的演算法為何，都會在標準結構中呈現採礦模型內容。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]提供的 Microsoft 一般內容樹狀檢視器中瀏覽此結構，然後切換到其中一個自訂檢視器，以查看該資訊是如何解譯及針對每一種模型類型來以圖形方式顯示。 您也可以針對採礦模型內容來建立查詢，其方式是使用支援 MINING_MODEL_CONTENT 結構描述資料列集的任何用戶端。 如需詳細資訊，請參閱 [資料採礦查詢工作和使用說明](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)。  
  
 本章節描述針對所有採礦模型類型所提供之內容的基本結構。 其中會描述所有採礦模型內容共同的節點類型，並提供如何解譯此資訊的指引。  
  
 [採礦模型內容的結構](#bkmk_Structure)  
  
 [模型內容中的節點](#bkmk_Nodes)  
  
 [依據演算法類型的採礦模型內容](#bkmk_AlgoType)  
  
 [檢視採礦模型內容的工具](#bkmk_Viewing)  
  
 [查詢採礦模型內容的工具](#bkmk_Querying)  
  
##  <a name="bkmk_Structure"></a> 採礦模型內容的結構  
 每一個模型的內容都會呈現為一系列的 *「節點」*(Node)。 節點是採礦模型內的一個物件，其中包含有關此模型之一部分的中繼資料和資訊。 節點會排列在階層中。 階層中節點的精確管理和階層的意義取決於您所使用的演算法而定。 例如，如果您建立決策樹模型，此模型可包含多個樹狀結構，全都連接到模型根；如果您建立類神經網路模型，此模型可包含一或多個其他網路，再加上統計資料節點。  
  
 每一個模型中的第一個節點稱為 *「根節點」*(Root Node) 或 *「模型父節點」* (Model Parent Node)。 每個模型都有根節點 (NODE_TYPE = 1)。 根節點通常包含了有關模型的一些中繼資料及子節點數目，但是很少包含此模型所找到之模式的其他相關資訊。  
  
 根據您用來建立模型的演算法而定，根節點具有各種不同的子節點數目。 子節點則具有不同的意義且包含了不同的內容 (根據演算法及資料的深度和複雜度而定)。  
  
##  <a name="bkmk_Nodes"></a> 採礦模型內容中的節點  
 在採礦模型中，節點是一般用途的容器，可儲存有關此模型的所有部分或一部分的資訊片段。 每一個節點的結構一定是相同的，而且包含了資料採礦結構描述資料列集所定義的資料行。 如需詳細資訊，請參閱 [DMSCHEMA_MINING_MODEL_CONTENT 資料列集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset)。  
  
 每一個節點都包含有關此節點的中繼資料，其中包含每一個模型內唯一的識別碼、父節點的識別碼，以及此節點擁有的子節點數目。 中繼資料會識別此節點所屬的模型以及特定模型儲存所在的資料庫目錄。 節點中所提供的其他內容將會因為用來建立模型的演算法類型而異，而且可能包含以下項目：  
  
-   支援特定預測值之定型資料內的案例計數。  
  
-   統計資料，例如平均值、標準差或變異數。  
  
-   係數和公式。  
  
-   規則和橫向指標的定義。  
  
-   描述模型之某部分的 XML 片段。  
  
### <a name="list-of-mining-content-node-types"></a>採礦內容節點類型的清單  
 下表列出當做資料採礦模型內之輸出的不同節點類型。 因為每一個演算法都會以不同方式處理資訊，所以每一個模型只會產生一些特定類型的節點。 如果您變更演算法，節點的類型可能會變更。 此外，如果您重新處理模型，每一個節點的內容都可能會變更。  
  
> [!NOTE]  
>  如果您使用不同的資料採礦服務，或建立您自己的外掛程式演算法，則可能會提供其他自訂節點類型。  
  
|NODE_TYPE 識別碼|節點標籤|節點內容|  
|-------------------|----------------|-------------------|  
|1|[模型]|中繼資料和根內容節點。 適用於所有模型類型。|  
|2|樹狀結構|分類樹狀結構的根節點。 適用於決策樹模型。|  
|3|Interior|樹狀結構內的內部分割節點。 適用於決策樹模型。|  
|4|Distribution|樹狀結構的終端節點。 適用於決策樹模型。|  
|5|叢集|演算法所偵測到的群集。 適用於叢集模型和時序叢集模型。|  
|6|Unknown|未知節點類型。|  
|7|ItemSet|演算法所偵測到的項目集。 適用於關聯模型或時序叢集模型。|  
|8|AssociationRule|演算法所偵測到的關聯規則。 適用於關聯模型或時序叢集模型。|  
|9|PredictableAttribute|可預測的屬性。 適用於所有模型類型。|  
|10|InputAttribute|輸入屬性。 適用於決策樹和貝氏機率分類模型。|  
|11|InputAttributeState|有關輸入屬性狀態的統計資料。 適用於決策樹和貝氏機率分類模型。|  
|13|序列|時序群集之 Markov 模型元件的最上層節點。 適用於時序叢集模型。|  
|14|Transition|Markov 轉換矩陣。 適用於時序叢集模型。|  
|15|TimeSeries|時間序列樹的非根節點。 僅適用於時間序列模型。|  
|16|TsTree|對應至可預測的時間序列之時間序列樹的根節點。 適用於時間序列模型 (只有當模型是使用 MIXED 參數所建立時)。|  
|17|NNetSubnetwork|一個子網路。 適用於類神經網路模型。|  
|18|NNetInputLayer|包含輸入層之節點的群組。 適用於類神經網路模型。|  
|19|NNetHiddenLayer|包含可描述隱藏層之節點的群組。 適用於類神經網路模型。|  
|21|NNetOutputLayer|包含輸出層之節點的群組。 適用於類神經網路模型。|  
|21|NNetInputNode|輸入層內符合具有對應狀態之輸入屬性的節點。 適用於類神經網路模型。|  
|22|NNetHiddenNode|隱藏層內的節點。 適用於類神經網路模型。|  
|23|NNetOutputNode|輸出層內的節點。 此節點通常會比對輸出屬性與對應的狀態。 適用於類神經網路模型。|  
|24|NNetMarginalNode|有關定型集的臨界統計資料。 適用於類神經網路模型。|  
|25|RegressionTreeRoot|迴歸樹的根節點。 適用於線性迴歸模型及包含連續輸入屬性的決策樹模型。|  
|26|NaiveBayesMarginalStatNode|有關定型集的臨界統計資料。 適用於貝氏機率分類模型。|  
|27|ArimaRoot|ARIMA 模型的根節點。 僅適用於使用 ARIMA 演算法的時間序列模型。|  
|28|ArimaPeriodicStructure|ARIMA 模型中的週期結構。 僅適用於使用 ARIMA 演算法的時間序列模型。|  
|29|ArimaAutoRegressive|ARIMA 模型內單一詞彙的自動迴歸係數。<br /><br /> 僅適用於使用 ARIMA 演算法的時間序列模型。|  
|30|ArimaMovingAverage|ARIMA 模型內單一詞彙的移動平均係數。 僅適用於使用 ARIMA 演算法的時間序列模型。|  
|1000|CustomBase|自訂節點類型的起點。 自訂節點類型必須是大於這個常數的整數值。 適用於使用自訂外掛程式演算法所建立的模型。|  
  
### <a name="node-id-name-caption-and-description"></a>節點識別碼、名稱、標題和描述  
 任何模型的根節點一定會有唯一識別碼 (**NODE_UNIQUE_NAME**) 0。 所有節點識別碼都是由 Analysis Services 自動指派，而且無法修改。  
  
 每一個模型的根節點也包含了有關此模型的一些基本中繼資料。 此中繼資料包含模型儲存所在的 Analysis Services 資料庫 (**MODEL_CATALOG**)、結構描述 (**MODEL_SCHEMA)**) 和模型的名稱 (**MODEL_NAME**)。 但是，此資訊會在模型的所有節點內重複，好讓您不需要查詢根節點，也可以取得此中繼資料。  
  
 除了當做唯一識別碼使用的名稱以外，每一個節點都有 *名稱* (**NODE_NAME**)。 此名稱是由演算法為了顯示所自動建立的，而且無法編輯。  
  
> [!NOTE]  
>  Microsoft 群集演算法可讓使用者為每一個群集指派易記名稱。 但是，這些易記名稱不會保存在伺服器上，而且如果您重新處理模型，此演算法將會產生新的群集名稱。  
  
 每一個節點的 *「標題」* (Caption) 和 *「描述」* (Description) 都是由演算法所自動產生，而且會當做標籤來幫助您了解節點的內容。 每一個欄位所產生的文字取決於模型類型。 在某些案例中，名稱、標題和描述可能會包含完全相同的字串，但是在某些模型中，描述可能會包含其他資訊。 請參閱有關個別模型類型的主題，以取得實作的詳細資料。  
  
> [!NOTE]  
>  只有當您使用可實作重新命名的自訂外掛程式演算法來建立模型時，Analysis Services 伺服器才會支援節點的重新命名。 若要啟用重新命名，當您建立外掛程式演算法時必須覆寫方法。  
  
### <a name="node-parents-node-children-and-node-cardinality"></a>父節點、子節點和節點基數  
 樹狀結構內父節點和子節點之間的關聯性是由 PARENT_UNIQUE_NAME 資料行的值所決定。 這個值會儲存在子節點內，並告訴您父節點的識別碼。 某些範例會遵循此資訊的可能使用方式：  
  
-   NULL 的 PARENT_UNIQUE_NAME 表示此節點是模型的最上層節點。  
  
-   如果 PARENT_UNIQUE_NAME 的值是 0，此節點必須是模型內最上層節點的直屬下階。 這是因為根節點的識別碼一定是 0。  
  
-   您可以使用資料採礦延伸模組 (DMX) 查詢內的函數來尋找特定節點的下階或上層。 如需在查詢中使用函數的詳細資訊，請參閱 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)。  
  
 *「基數」* (Cardinality) 指定是集合內的項目數。 在已處理之採礦模型的內容中，基數會告訴您特定節點中的子節點數目。 例如，如果決策樹模型有一個 [Yearly Income] 的節點，而該節點有兩個子節點，一個是條件 [Yearly Income] = High 的節點，另一個是條件 [Yearly Income] = Low 的節點，則 [Yearly Income] 節點的 CHILDREN_CARDINALITY 值會是 2。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，只有在計算節點的基數時才會計算直屬子節點。 但是，如果您建立自訂外掛程式演算法，可以多載 CHILDREN_CARDINALITY 來以不同方式計算基數。 例如，如果您想要計算下階的總數，而不只是直屬子節點，這個處理方式可能會很實用。  
  
 雖然所有模型都會以相同方式來計算基數，但是您解譯或使用基數值的方式則會因模型類型而異。 例如在叢集模型中，最上層節點的基數會告訴您找到的叢集總數。 在其他類型的模型中，基數可能會一直有一個設定的值 (取決於節點類型)。 如需有關如何解譯基數的詳細資訊，請參閱有關個別模型類型的主題。  
  
> [!NOTE]  
>  某些模型 (例如 Microsoft 類神經網路演算法所建立的模型) 會額外包含一個特殊節點類型，該類型會針對整個模型提供有關定型資料的描述性統計資料。 就定義來說，這些節點永遠不會有子節點。  
  
### <a name="node-distribution"></a>node distribution  
 NODE_DISTRIBUTION 資料行包含一個巢狀資料表，在許多節點中，該資料表會提供有關演算法找到之模式的重要詳細資訊。 此資料表中提供的精確統計資料取決於模型類型、樹狀結構內的節點位置，以及可預測的屬性是連續數值還是離散值而定；但是，它們可包含屬性的最小值和最大值、指派給值的加權、節點內的案例數、迴歸公式內使用的係數，以及統計量值 (如標準差和變異數)。 如需有關如何解譯節點分佈的詳細資訊，請參閱有關您所使用之特定模型類型的主題。  
  
> [!NOTE]  
>  NODE_DISTRIBUTION 資料表可能是空的 (視節點類型而定)。 例如，某些節點只會用來組織子節點的集合，而包含詳細統計資料的就是子節點。  
  
 巢狀資料表 NODE_DISTRIBUTION 一定會包含以下資料行。 每一個資料行的內容都會因模型類型而異。 如需有關特定模型類型的詳細資訊，請參閱「 [依據演算法類型的採礦模型內容](#bkmk_AlgoType)」。  
  
 ATTRIBUTE_NAME  
 內容會因演算法而異。 它可以是資料行的名稱 (如可預測的屬性、規則、項目集) 或是演算法內部的資訊片段 (如公式的一部分)。  
  
 這個資料行也可以包含屬性-值配對。  
  
 ATTRIBUTE_VALUE  
 ATTRIBUTE_NAME 中命名之屬性的值。  
  
 如果此屬性名稱是資料行，則在最直接的案例中，ATTRIBUTE_VALUE 會包含該資料行的其中一個離散值。  
  
 根據演算法處理值的方式而定，ATTRIBUTE_VALUE 也可以包含一個旗標，告訴您屬性 (**Existing**) 是否有值存在，或者該值是否為 null (**Missing**)。  
  
 例如，如果已設定您的模型來尋找已購買某個特定項目至少一次的客戶，則 ATTRIBUTE_NAME 資料行可能會包含屬性-值配對來定義想要的項目 (例如 `Model = 'Water bottle'`)，而且 ATTRIBUTE_VALUE 資料行只會包含關鍵字 **Existing** 或 **Missing**。  
  
 SUPPORT  
 具有這個屬性-值配對或是包含此項目集或規則的案例數。  
  
 一般對每個節點而言，support 值都會告訴您目前節點中包含的定型集內有多少案例。 在大多數的模型類型中，support 代表明確的案例數。 Support 值很實用是因為您可以在定型案例內檢視資料的分佈，而不必查詢定型資料。 Analysis Services 伺服器也會使用這些儲存值來計算儲存的機率與之前的機率，以判斷推斷是強的還是弱的。  
  
 例如在分類樹狀結構中，support 值表示具有描述之屬性組合的案例數。  
  
 在決策樹中，樹狀結構每一層的 support 總和是其父節點的 support 總和。 例如，如果包含 1200年個案例的模型是依性別，平均分配，然後再依收入低、 中度和高的子節點的節點 (2)，也就是節點 (4)、 (5) 的三個值和 (6)，一律加總為節點 (2) 相同的案例數目。  
  
|節點識別碼和節點屬性|支持度計數|  
|---------------------------------|-------------------|  
|(1) Model root|1200|  
|(2) Gender = Male<br /><br /> (3) Gender = Female|600<br /><br /> 600|  
|(4) Gender = Male 且 Income = High<br /><br /> (5) Gender = Male 且 Income = Medium<br /><br /> (6) Gender = Male 且 Income = Low|200<br /><br /> 200<br /><br /> 200|  
|(7) Gender = Female 且 Income = High<br /><br /> (8) Gender = Female 且 Income = Medium<br /><br /> (9) Gender = Female 且 Income = Low|200<br /><br /> 200<br /><br /> 200|  
  
 如果是叢集模型，可以加權 support 數目，以包含屬於多個叢集的機率。 多個群集成員資格是預設的群集方法。 在此情況下，因為每一個案例不一定都只會屬於一個群集，所以這些方法中的 support 可能不會在所有群集中加總到百分之 100。  
  
 PROBABILITY  
 表示這個特定節點在整個模型內的機率。  
  
 一般來說，機率代表這個特定值的 support 除以節點內的案例總數 (NODE_SUPPORT)。  
  
 但是，機率會稍微調整過，以去除資料內的遺漏值所造成的偏誤。  
  
 例如，如果 [Total Children] 目前的值為 'One' 和 'Two'，您會想要避免建立一個預測出無法有任何子節點或是有三個子節點的模型。 為了確保遺漏的值不是必然的，但也不是不可能，演算法會在任何屬性的實際值計數中加上 1。  
  
 範例  
  
 Probability of [Total Children = One] = [Count of cases where Total Children = One] + 1/[Count of all cases] + 3  
  
 Probability of [Total Children = Two]= [Count of cases where Total Children = Two] +1/[Count of all cases] +3  
  
> [!NOTE]  
>  3 的調整是由現有值的總數 n 加上 1 計算而來。  
  
 在調整之後，所有值的機率仍然會加上 1。 沒有任何資料之值的機率 (在此範例中，[Total Children ='Zero', 'Three', 或某個其他值]) 會從非常低的非零值開始，並隨著案例的增加而緩慢上升。  
  
 variance  
 表示節點內值的變異數。 就定義來說，離散值的變異數一定是 0。 如果模型支援連續值，變異數會計算為 (sigma)，其方式是使用分母 n 或節點中的案例數。  
  
 一般會使用兩種定義來代表標準差 (**StDev**)。 計算標準差的一個方法會將偏誤列入考量，另一個方法在計算標準差時則不會考量偏誤。 一般來說，Microsoft 資料採礦演算法在計算標準差時，並不會使用偏誤。  
  
 NODE_DISTRIBUTION 資料表中出現的值為所有離散和離散化屬性的實際值及連續值的平均值。  
  
 VALUE_TYPE  
 表示值或屬性的資料類型及值的使用方式。 某些值類型只適用於某些模型類型：  
  
|VALUE_TYPE 識別碼|值標籤|值類型名稱|  
|--------------------|-----------------|---------------------|  
|1|Missing|表示案例資料不包含這個屬性的值。 在計算 **Missing** 狀態時，會與具有值的屬性分開。|  
|2|Existing|表示案例資料包含這個屬性的值。|  
|3|Continuous|表示屬性值是一個連續數值，因此可以由平均值連同變異數和標準差來表示。|  
|4|Discrete|表示一個視為離散的值 (數值或文字)。<br /><br /> **注意** ：Discrete 值也可以是 missing 值；但是在計算時會以不同方式處理這兩個值。 如需相關資訊，請參閱[遺漏值 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md)。|  
|5|Discretized|表示此屬性包含已經離散化的數值。 此值將會是一個描述離散化值區的格式化字串。|  
|6|Existing|表示此屬性具有連續數值，而且資料中已經提供值 (遺漏或推斷的值)。|  
|7|Coefficient|表示代表著係數的數值。<br /><br /> 係數是計算相依變數的值時所套用的值。 例如，如果您的模型建立一個迴歸公式來根據年齡預測收入，則讓年齡與收入產生關聯的公式中會使用係數。|  
|8|Score gain|表示代表著屬性之得分的數值。|  
|9|統計資料|表示代表著迴歸輸入變數之統計資料的數值。|  
|10|Node unique name|表示此值不應該處理為數值或字串，而是要處理為模型內另一個內容節點的唯一識別碼。<br /><br /> 例如在類神經網路模型中，識別碼會提供從輸出層內之節點指向隱藏層內節點的指標，並提供從隱藏層內之節點指向輸入層內之節點的指標。|  
|11|Intercept|表示代表著迴歸公式內之攔截的數值。|  
|12|Periodicity|表示代表模型內之週期性結構的值。<br /><br /> 僅適用於包含 ARIMA 模型的時間序列模型。<br /><br /> 注意:Microsoft 時間序列演算法會自動偵測週期性結構的定型資料。 因此，最終模型內的週期性可能包含當您建立模型時未當做參數提供的週期性值。|  
|13|Autoregressive order|表示代表著自動迴歸數列數目的值。<br /><br /> 適用於使用 ARIMA 演算法的時間序列模型。|  
|14|Moving average order|表示代表著數列中移動平均數目的值。<br /><br /> 適用於使用 ARIMA 演算法的時間序列模型。|  
|15|Difference order|表示代表著數列差異化之次數的值。<br /><br /> 適用於使用 ARIMA 演算法的時間序列模型。|  
|16|布林|表示布林類型。|  
|17|其他|表示演算法所定義的自訂值。|  
|18|Prerendered string|表示演算法轉譯為字串的自訂值。 物件模型未套用任何格式。|  
  
 此數值類型是衍生自 ADMOMD.NET 列舉。 如需詳細資訊，請參閱 <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>(Mining Model Content)。  
  
### <a name="node-score"></a>節點分數  
 節點分數的意義因模型類型而異，而且可能也是節點類型所特有。 如需如何針對每一個模型和節點類型計算 NODE_SCORE 的相關資訊，請參閱 [依據演算法類型的採礦模型內容](#bkmk_AlgoType)。  
  
### <a name="node-probability-and-marginal-probability"></a>節點機率和臨界機率  
 採礦模型結構描述資料列集針對所有模型類型包含 NODE_PROBABILITY 和 MARGINAL_PROBABILITY 資料行。 這些資料行只有在機率值有意義的節點中才會包含值。 例如，模型的根節點絕對不會包含機率分數。  
  
 在提供機率分數的節點中，節點機率和臨界機率代表不同的計算。  
  
-   **臨界機率** ：為從節點的父節點到達節點的機率。  
  
-   **節點機率** ：為從根節點到達節點的機率。  
  
-   **節點機率** ：一定會小於或等於 **臨界機率**。  
  
 例如，如果決策樹中所有客戶的母體擴展依性別均分 (而且沒有遺漏任何值)，則子節點的機率應該是 5。 不過，假設每個節點的性別會平均分配依收入等級為高、 中和低。 在此情況下，每一個子節點的 MARGINAL_PROBABILITY 分數應該是 .33，但是 NODE_PROBABILTY 值將會是導致該節點之所有機率的乘積，因此一定小於 MARGINAL_PROBABILITY 值。  
  
|節點/屬性的等級和值|臨界機率|節點機率|  
|----------------------------------------|--------------------------|----------------------|  
|模型根<br /><br /> 所有目標客戶|1|1|  
|依性別分割的目標客戶|.5|.5|  
|依性別分割，然後再依收入分成三等級的目標客戶。|.33|.5 * .33 = .165|  
  
### <a name="node-rule-and-marginal-rule"></a>節點規則與臨界規則  
 採礦模型結構描述資料列集也會針對所有模型類型包含 NODE_RULE 和 MARGINAL_RULE 資料行。 這些資料行包含用來序列化模型及代表模型結構之某部分的 XML 片段。 這些資料行對於某些節點來說可能是空白的 (如果值無意義的話)。  
  
 提供兩種 XML 規則，類似於兩種機率值。 MARGINAL_RULE 中的 XML 片段會定義目前節點的屬性和值，而 NODE_RULE 中的 XML 片段則會描述從模型根到目前節點的路徑。  
  
##  <a name="bkmk_AlgoType"></a> 依據演算法類型的採礦模型內容  
 每一個演算法都會在它的內容結構描述中儲存不同類型的資訊。 例如， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法會產生許多子節點，每一個子節點都代表可能的群集。 每一個叢集節點都包含可描述群集中項目共用之特性的規則。 相較之下， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法則不會包含任何子節點；而模型的父節點會包含可描述分析所找到之線性關聯性的方程式。  
  
 下表提供每一種演算法之主題的連結。  
  
-   **模型內容主題：** 說明針對每一個演算法類型，每個節點類型的意義，並且提供哪些節點屬於在特定模型類型中最有用的指引。  
  
-   **查詢主題：** 提供有關如何解譯結果的查詢，針對特定模型類型和指引的範例。  
  
|演算法或模型類型|model content|查詢採礦模型|  
|-----------------------------|-------------------|----------------------------|  
|關聯規則模型|[關聯模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)|[關聯模型查詢範例](../../analysis-services/data-mining/association-model-query-examples.md)|  
|叢集模型|[決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[群集模型查詢範例](../../analysis-services/data-mining/clustering-model-query-examples.md)|  
|決策樹模型|[決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[決策樹模型查詢範例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)|  
|線性迴歸模型|[線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)|[線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|羅吉斯迴歸模型|[羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)|[線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|貝氏機率分類模型|[貝氏機率分類模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)|[Naive Bayes Model Query Examples](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)|  
|類神經網路模型|[類神經網路模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)|[Neural Network Model Query Examples](../../analysis-services/data-mining/neural-network-model-query-examples.md)|  
|時序群集|[時序叢集模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)|[Sequence Clustering Model Query Examples](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)|  
|時間序列模型|[時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|[時間序列模型查詢範例](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
##  <a name="bkmk_Viewing"></a> 檢視採礦模型內容的工具  
 當您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中瀏覽或探索模型時，可以在 **[Microsoft 一般內容樹狀檢視器]** 中檢視資訊，此工具在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中都有提供。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容檢視器會使用採礦模型的內容結構描述資料列集中提供的相同資訊，顯示資料行、規則、屬性 (Property)、屬性 (Attribute)、節點和其他內容。 內容結構描述資料列集是一般性架構，用來展示有關資料採礦模型內容的詳細資訊。 您可以在任何支援階層式資料列集的用戶端中檢視模型內容。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的檢視器會在 HTML 表格檢視器中呈現此資訊，以一致的格式表示所有模型，讓您更容易了解您所建立之模型的結構。 如需詳細資訊，請參閱 [使用 Microsoft 一般內容樹狀檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
##  <a name="bkmk_Querying"></a> 查詢採礦模型內容的工具  
 若要擷取採礦模型內容，您必須針對資料採礦模型建立查詢。  
  
 建立內容查詢之最簡單的方法就是在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中執行以下 DMX 陳述式：  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 如需詳細資訊，請參閱 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)。  
  
 您也可以使用資料採礦結構描述資料列集來查詢採礦模型內容。 結構描述資料列集是一種標準結構，用戶端可用它來探索、瀏覽及查詢有關採礦結構和模型的資訊。 您也可以使用 XMLA、Transact-SQL 或 DMX 陳述式來查詢結構描述資料列集。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您也可以存取資料採礦結構描述資料列集中的資訊，其方式是開啟 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的連接及查詢系統資料表。 如需詳細資訊，請參閱 [資料採礦結構描述資料列集 &#40;SSAs&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  
