---
title: "Microsoft 類神經網路演算法技術參考 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- HIDDEN_NODE_RATIO parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- HOLDOUT_PERCENTAGE parameter
- neural network algorithms [Analysis Services]
- output layer [Data Mining]
- neural networks
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- hidden layer
- hidden neurons
- input layer [Data Mining]
- activation function [Data Mining]
- Back-Propagated Delta Rule network
- neural network model [Analysis Services]
- coding [Data Mining]
- HOLDOUT_SEED parameter
ms.assetid: b8fac409-e3c0-4216-b032-364f8ea51095
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 46dc639d30a60ef8f332c340e3ffd685c8f4f72f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="microsoft-neural-network-algorithm-technical-reference"></a>Microsoft Neural Network Algorithm Technical Reference
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路使用「多層認知」(Multilayer Perceptron) 網路，亦稱為「倒傳播差異規則」(Back-Propagated Delta Rule) 網路，它包含最多 3 層神經 (Neuron) 或「認知器」(Perceptron)。 這 3 層分別是輸入層、選擇性隱藏層和輸出層。  
  
 多層認知類神經網路的詳細討論是在此文件集的範圍之外。 本主題說明演算法的基本實作，包括將輸入和輸出值正規化所使用的方法，以及減少屬性基數所使用的特徵選取方法。 本主題描述自訂演算法行為所使用的參數及其他設定，並提供關於查詢模型之其他資訊的連結。  
  
## <a name="implementation-of-the-microsoft-neural-network-algorithm"></a>Microsoft 類神經網路演算法的實作  
 在多層認知類神經網路上，每一層神經會接收一或多個輸入，並會產生一或多個相同的輸出。 每一個輸出就是神經輸入總和的簡易非線性函數。 輸入會從輸入層的節點向前傳遞到隱藏層的節點，然後再從隱藏層傳遞至輸出層；同一層內的神經之間沒有連接 如果不包括隱藏層，則輸入會直接從輸入層的節點向前傳遞到輸出層的節點中，就像在羅吉斯迴歸模型一樣。  
  
 在以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法建立的類神經網路中，有 3 種神經類型：  
  
**輸入神經**  
  
 輸入神經會提供資料採礦模型的輸入屬性值。 針對離散輸入屬性，輸入神經通常代表輸入屬性的單一狀態。 如果該屬性的定型資料包含 Null 值，這就包含遺漏值。 有兩個以上之狀態的分散輸入屬性會為每一個狀態產生一個輸入神經，如果定型資料中有任何 Null 值，則為遺漏狀態產生一個輸入神經。 連續輸入屬性會產生兩個輸入神經：一個神經用於遺漏狀態，而另一個神經用於連續屬性本身的值。 輸入神經會提供輸入給一或多個隱藏神經。  
  
**Hidden neurons**  
  
 隱藏神經會接收來自輸入神經的輸入，並提供輸出給輸出神經。  
  
**輸出神經**  
  
 輸出神經代表資料採礦模型的可預測屬性值。 針對分隔輸入屬性，輸出神經通常代表可預測屬性的單一預測狀態，包括遺漏值。 例如，二進位可預測屬性會產生一個描述遺漏狀態或現有狀態的輸出節點，指出該屬性的值是否存在。 用來做為可預測屬性的布林資料行會產生 3 個輸出神經：一個用於 True 值的神經，一個用於 False 值的神經，以及一個用於遺漏狀態或現有狀態的神經。 有兩個以上之狀態的分隔可預測屬性會為每一個狀態產生一個輸出神經，並為遺漏狀態或現有狀態產生一個輸出神經。 連續可預測資料行會產生兩個輸出神經：一個用於遺漏狀態或現有狀態的神經，一個用於連續資料行值本身的神經。 如果透過檢閱可預測資料行集產生的輸出神經超過 500 個， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會在採礦模型中產生新網路來代表其他輸出神經。  
  
 神經會接收其他神經或其他資料的輸入，端視該神經位於網路的哪一層而定。 輸入神經會接收來自原始資料的輸入。 隱藏神經和輸出神經會接收類神經網路中，來自其他神經輸出的輸入。 輸入會建立神經之間的關聯性，而關聯性會做為特定案例集分析的路徑。  
  
 每一個輸入都有被指派一個值，稱為 *「加權」*(Weight)，它描述該特定輸入對隱藏神經或輸出神經的相關性或重要性。 指派給輸入的加權越大，該輸入之值的相關性或重要性就越大。 加權可以是負數，這表示輸入可以禁止而非啟動特定神經。 每個輸入的值會乘以加權來強調特定神經之輸入的重要性。 若為負加權，值乘以加權的結果表示不強調重要性。  
  
 每一個神經都有被指派一個簡易非線性函數，稱為「啟用函數」，它描述特定神經對該類神經網路層的相關性或重要性。 隱藏神經會對其啟用函數使用「雙曲線正切」函數 (tanh)，而輸出神經則會對其啟用函數使用「S 型」(sigmoid) 函數。 兩個函數都是非線性連續函數，可讓類神經網路建立輸入和輸出神經之間的非線性關聯性模型。  
  
### <a name="training-neural-networks"></a>培訓類神經網路  
 培訓使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法的資料採礦模型，包括數個步驟。 您針對演算法參數所指定的值，對這些步驟會有很大的影響。  
  
 演算法會先從資料來源評估和擷取定型資料。 定型資料的百分比稱為 *「鑑效組資料」*(Holdout Data)，保留供評估網路的精確度之用。 在整個定型程序期間，定型資料的每一次反覆之後，網路就會立即接受評估。 當精確度不再增加時，定型程序即停止。  
  
 *SAMPLE_SIZE* 和 *HOLDOUT_PERCENTAGE* 參數的值用於決定從定型資料取樣的案例數目，以及針對鑑效組資料暫擱的案例數目。 *HOLDOUT_SEED* 參數的值用於隨機決定針對鑑效組資料而暫擱的個別案例。  
  
> [!NOTE]  
>  這些演算法參數與 HOLDOUT_SIZE 和 HOLDOUT_SEED 屬性不同，後兩者適用於採礦結構，藉以定義測試資料集。  
  
 接下來，演算法會決定採礦模型支援的網路數目和複雜度。 如果採礦模型包含一或多個只用於預測的屬性，則演算法會建立單一網路來代表所有這些屬性。 如果採礦模型包含一或多個同時用於輸入和預測的屬性，則演算法提供者會為每一個屬性建構網路。  
  
 針對具有離散值的輸入屬性和可預測屬性，每一個輸入或輸出神經分別代表單一狀態。 針對具有連續值的輸入屬性和可預測屬性，每一個輸入或輸出神經分別代表該屬性值的範圍和散發。 在任一案例中所支援的最大狀態數目，會視 *MAXIMUM_STATES* 演算法參數的值而定。 如果特定屬性的狀態數目超過 *MAXIMUM_STATES* 演算法參數的值，則會選擇該屬性最常用或最相關的狀態 (不超過允許的最大狀態數目)，而其餘狀態則會分成遺漏值群組，作為分析用途。  
  
 然後，決定要為隱藏層建立的初始神經數目時，演算法會使用 *HIDDEN_NODE_RATIO* 參數的值。 您可以將 *HIDDEN_NODE_RATIO* 設定為 0，以防止在網路中建立演算法為採礦模型所產生的隱藏層，而將類神經網路視為邏輯迴歸來處理。  
  
 演算法提供者反覆地同時評估網路上所有輸入的加權，使用先前保留的培訓資料集，以及將鑑效組資料中每一個案例的實際已知值與網路的預測做比較，這種程序稱為 *批次學習*。 在演算法評估整個培訓資料集之後，演算法會檢閱每一個神經的預測值和實際值。 演算法會計算錯誤的程度 (如果有的話) 並調整與該神經的輸入相關聯的加權，從輸出神經回溯到輸入神經，這種程序稱為 *倒傳播*。 接著，演算法會對整個培訓資料集重複此程序。 因為演算法可以支援許多加權和輸出神經，所以使用結合漸層演算法 (conjugate gradient algorithm) 來引導培訓程序，以指派和評估輸入的加權。 結合漸層演算法的討論超出此文件集的範圍之外。  
  
### <a name="feature-selection"></a>特徵選取  
 如果輸入屬性的數目大於 *MAXIMUM_INPUT_ATTRIBUTES* 參數的值，或者如果可預測屬性的數目大於 *MAXIMUM_OUTPUT_ATTRIBUTES* 參數的值，則會使用特徵選取演算法來降低包含在採礦模型中之網路的複雜度。 特徵選取會將輸入屬性或可預測屬性的數目減少為在統計上與模型最相關的數目。  
  
 所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦演算法都會自動使用特徵選取來改善分析並減少處理的負載。 在類神經網路模型中，特徵選取所使用的方法取決於屬性的資料類型。 下表顯示用於類神經網路模型的特徵選取方法，並同時顯示用於羅吉斯迴歸演算法 (以類神經網路演算法為基礎) 的特徵選取方法，做為參考。  
  
|演算法|分析的方法|註解|  
|---------------|------------------------|--------------|  
|類神經網路|有趣性分數<br /><br /> Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|類神經網路演算法可以使用以熵為基礎的計分方法和貝氏計分方法，只要資料包含連續資料行即可。<br /><br /> 預設值。|  
|羅吉斯迴歸|有趣性分數<br /><br /> Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|因為您無法將參數傳遞給這個演算法來控制特徵選取行為，所以會使用預設值。 因此，如果所有屬性都是離散或離散化的，則預設值為 BDEU。|  
  
 針對類神經網路模型控制特徵選取的演算法參數為 MAXIMUM_INPUT_ATTRIBUTES、MAXIMUM_OUTPUT_ATTRIBUTES 和 MAXIMUM_STATES。 您也可以設定 HIDDEN_NODE_RATIO 參數，以控制隱藏層的數目。  
  
### <a name="scoring-methods"></a>計分方法  
 *「計分」* (Scoring) 是一種正規化，在定型類神經網路模型的內容中表示一種程序，會將離散文字標籤之類的值轉換為可以與網路中其他輸入類型比較並加權的值。 例如，如果其中一個輸入屬性為 Gender，且可能的值為 Male 和 Female，而另一個輸入屬性為 Income，且包含值的變數範圍，則每個屬性的值無法直接比較，因此必須編碼為一般小數位數，讓加權可以計算。 計分是將此類輸入正規化為數值的程序：特別是正規化為機率範圍。 用於正規化的函數也有助於針對統一的比例，更平均地散發輸入值，如此一來，極端值就不會扭曲分析的結果。  
  
 類神經網路的輸出也會經過編碼。 當輸出 (也就是預測) 有一個單一目標，或有僅用於預測，而不用於輸入的多個目標時，模型會建立一個單一網路，而且它可能不需要將值正規化。 不過，如果輸入和預測使用多個屬性，模型必須建立多個網路，因此，所有值都必須正規化，而且在離開網路時，也必須將輸出編碼。  
  
 輸入的編碼是以定型案例中每個離散值的總和為基礎，然後將該值乘以其加權。 這就是所謂的 *「加權總和」*(Weighted Sum)，這個加權總和會傳遞到隱藏層中的啟用函數。 Z-score 用於編碼，如下所示：  
  
 **離散值**  
  
 `μ = p` (狀態的優先機率)  
  
 `StdDev  = sqrt(p(1-p))`  
  
 **連續值**  
  
 目前的值 = `1 - μ/σ`  
  
 無現有值 = `-μ/σ`  
  
 這些值經過編碼之後，輸入會以網路邊緣當做加權，進行加權總和。  
  
 輸出的編碼使用 sigmoid 函數，其中包含的屬性對於預測相當實用。 其中一個這種屬性是，不管如何調整原始值，也不管是負值還是正值，此函數的輸出永遠是介於 0 和 1 的值，也就是適合評估機率的值。 其他實用的屬性是，sigmoid 函數具備緩衝效果，因此，當這些值與轉折點的距離比較遠時，該值的機率就會向前移到 0 或 1，但是移動速度很緩慢。  
  
## <a name="customizing-the-neural-network-algorithm"></a>自訂類神經網路演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法支援數個會影響所產生之採礦模型的行為、效能和精確度的參數。 您也可以在資料行上設定模型旗標，或設定散發旗標來指定如何處理資料行內的值，藉以修改模型處理資料的方式。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 下表描述可搭配 Microsoft 類神經網路演算法使用的參數。  
  
 HIDDEN_NODE_RATIO  
 指定隱藏神經與輸入和輸出神經的比例。 下列公式決定隱藏層中的初始神經數目：  
  
 HIDDEN_NODE_RATIO * SQRT(總輸入神經 \* 總輸出神經)  
  
 預設值為 4.0。  
  
 HOLDOUT_PERCENTAGE  
 指定用來計算鑑效組錯誤之定型資料內的案例百分比，這可作為定型採礦模型時停止準則的一部分。  
  
 預設值是 30。  
  
 HOLDOUT_SEED  
 在演算法隨機決定鑑效組資料時，指定用來植入虛擬隨機產生器的數字。 如果此參數設定為 0，此演算法會依據採礦模型的名稱產生種子，以保證在重新處理期間，模型內容保持不變。  
  
 預設值是 0。  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 決定在運用特徵選取之前可提供給演算法之輸入屬性的最大數目。 將此值設定為 0，會停用輸入屬性的特徵選取。  
  
 預設值為 255。  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 決定在運用特徵選取之前可提供給演算法之輸出屬性的最大數目。 將此值設定為 0，會停用輸出屬性的特徵選取。  
  
 預設值為 255。  
  
 MAXIMUM_STATES  
 指定演算法支援的每個屬性之離散狀態的最大數目。 如果特定屬性的狀態數目大於針對這個參數所指定的數字，則演算法會使用該屬性最常用的狀態，並將其餘狀態視為遺漏。  
  
 預設值為 100。  
  
 SAMPLE_SIZE  
 指定用來定型模型的案例數目。 此演算法會使用此數字或不包括在鑑效組資料中之總案例數的百分比 (由 HOLDOUT_PERCENTAGE 參數指定)，以較小者為準。  
  
 換句話說，如果 HOLDOUT_PERCENTAGE 設定為 30，則演算法將使用這個參數的值或等於總案例數 70% 的值，以較小者為準。  
  
 預設值為 10000。  
  
### <a name="modeling-flags"></a>模型旗標  
 系統支援下列模型旗標，可搭配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法使用。  
  
 NOT NULL  
 表示資料行不能包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。  
  
 適用於採礦結構資料行。  
  
 MODEL_EXISTENCE_ONLY  
 表示模型應該只考量屬性的值是否存在，或者值是否遺漏。 確實的值不相符。  
  
 適用於採礦模型資料行。  
  
### <a name="distribution-flags"></a>散發旗標  
 系統支援下列散發旗標，可搭配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法使用。 旗標只能當做模型的提示使用；如果演算法偵測到不同的散發，它將會使用找到的散發，而不是提示中提供的散發。  
  
 一般  
 表示資料行內的值應該被視為它們代表正常或高斯、散發。  
  
 Uniform  
 表示資料行內的值應該被視為它們以統一的方式散發，也就是說，任何值的機率都大致相等，而且是值總數的函數。  
  
 Log Normal  
 表示資料行內的值應視為根據「對數常態」曲線分佈，也就是說值的對數會以常態方式分佈。  
  
## <a name="requirements"></a>需求  
 類神經網路模型必須至少包含一個輸入資料行和一個輸出資料行。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法支援下表所列的特定輸入資料行和可預測資料行。  
  
|資料行|內容類型|  
|------------|-------------------|  
|輸入屬性|Continuous、Cyclical、Discrete、Discretized、Key、Table 和 Ordered|  
|可預測屬性|Continuous、Cyclical、Discrete、Discretized 和 Ordered|  
  
> [!NOTE]  
>  系統支援 Cyclical 和 Ordered 內容類型，但是演算法將它們視為離散值，因此不會執行特殊處理。  
  
## <a name="see-also"></a>請參閱＜  
 [Microsoft 類神經網路演算法](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [類神經網路模型 &#40; 的採礦模型內容Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [類神經網路模型查詢範例](../../analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  
