---
title: Microsoft 羅吉斯迴歸演算法技術參考 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- logistic regression [Analysis Services]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- HOLDOUT_PERCENTAGE parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- regression algorithms [Analysis Services]
- HOLDOUT_SEED parameter
ms.assetid: cf32f1f3-153e-476f-91a4-bb834ec7c88d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 157baeb7e5bd8fb53b2435f55e3e71c098632002
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733918"
---
# <a name="microsoft-logistic-regression-algorithm-technical-reference"></a>Microsoft 羅吉斯迴歸演算法技術參考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 羅吉斯迴歸演算法是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 類神經網路演算法的演變，其中 *HIDDEN_NODE_RATIO* 參數設為 0。 此設定會建立不包含隱藏層的類神經網路模型，而這相等於羅吉斯迴歸。  
  
## <a name="implementation-of-the-microsoft-logistic-regression-algorithm"></a>Microsoft 羅吉斯迴歸演算法的實作  
 假設可預測資料行只包含兩個狀態，但您仍然想要執行迴歸分析，使輸入資料行與可預測資料行將包含特定狀態的機率相關。 下列圖表說明如果您指定 1 和 0 給可預測資料行的狀態時將得到的結果，請計算資料行將包含特定狀態的機率，並對輸入屬性執行線性迴歸。  
  
 ![模式化不良資料使用線性迴歸](../media/logistic-linear-regression.gif "模式化不良資料使用線性迴歸")  
  
 x 軸包含輸入資料行的值。 y 軸包含可預測資料行成為一個狀態或另一個狀態的機率。 其問題在於，即使 0 和 1 是資料行的最大值和最小值，但線性迴歸並不限制資料行介於 0 和 1 之間。 解決此問題的方式之一是執行羅吉斯迴歸。 羅吉斯迴歸分析不建立直線，而是建立「S」形曲線來包含最大和最小條件約束。 例如，下列圖表說明您如果對先前範例所使用的相同資料執行羅吉斯迴歸會達到的結果。  
  
 ![資料模型化使用羅吉斯迴歸](../media/logistic-regression.gif "資料建立使用羅吉斯迴歸模型")  
  
 請注意，曲線絕不能高於 1 或低於 0。 您可以使用羅吉斯迴歸來描述哪些輸入資料行在決定可預測資料行的狀態時很重要。  
  
### <a name="feature-selection"></a>特徵選取  
 所有 Analysis Services 資料採礦演算法都會自動使用特徵選取來改善分析並減少處理的負載。 在羅吉斯迴歸模型中，特徵選取所使用的方法取決於屬性的資料類型。 羅吉斯迴歸是以 Microsoft 類神經網路演算法為基礎，因此，它會使用適用於類神經網路的特徵選取方法子集。 如需詳細資訊，請參閱[特徵選取 &#40;資料採礦&#41;](feature-selection-data-mining.md)。  
  
### <a name="scoring-inputs"></a>計分輸入  
 在類神經網路模型或羅吉斯迴歸模型的內容中，「計分」表示一種程序，會將資料中出現的值轉換為使用相同小數位數的一組值，因此可以互相比較。 例如，假設 Income 輸入的範圍是 0 到 100,000，而 [Number of Children] 輸入的範圍是 0 到 5。 此轉換程序可讓您*分數*，或比較，不論值的差異的每個輸入的重要性。  
  
 對於出現在定型集中的每個狀態，模型都會產生一個輸入。 對於離散或離散化的輸入，如果在定型集中至少出現一次遺漏狀態，則會建立其他輸入來代表「遺漏」狀態。 至於連續輸入，最多會建立兩個輸入節點：一個用於「遺漏」值 (如果出現在定型資料中)，而另一個輸入則用於所有現有的值或非 Null 值。 每個輸入會調整為數值的格式使用 z-score 正規化方法，(x-μ） / 標準差。  
  
 在 z-score 正規化期間，平均值 (μ) 和標準差會透過完整的定型集取得。  
  
 **連續值**  
  
 值會出現： (X-μ)/σ / / X 是要編碼的實際值)  
  
 值不存在:-μ/σ / / 負平均值除以標準差)  
  
 **離散值**  
  
 Μ = p-（狀態的優先機率）  
  
 StdDev  = sqrt(p(1-p))  
  
 值會出現：   (1-μ)/σ / / (1 減平均值) 除以標準差)  
  
 值不存在: (-μ) / σ / / 負平均值除以標準差)  
  
### <a name="understanding-logistic-regression-coefficients"></a>了解羅吉斯迴歸係數  
 在統計文獻中，有各種方法可以執行羅吉斯迴歸，但是所有方法的重要部分都是評估模型的符合度。 在勝算比和共變模式之間，提出各種符合程度統計資料。 如何測量模型符合度的討論超出本主題的範圍，不過，您可以在模型中擷取係數的值，然後用於設計符合您自己的量值。  
  
> [!NOTE]  
>  當做羅吉斯迴歸模型一部分建立的係數不代表勝算比，而且不應該如此解譯。  
  
 模型圖形中每個節點的係數都代表該節點之輸入的加權總和。 在羅吉斯迴歸模型中，隱藏層是空的，因此只有輸出節點中儲存的一組係數。 您可以使用下列查詢來擷取係數的值：  
  
```  
SELECT FLATTENED [NODE_UNIQUE NAME],  
(SELECT ATTRIBUTE_NAME< ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) AS t  
FROM <model name>.CONTENT  
WHERE NODE_TYPE = 23  
```  
  
 針對每個輸出值，此查詢會傳回係數以及指回相關輸入節點的識別碼。 它也會傳回包含輸出值與截距的資料列。 每個輸入 X 都有自己的係數 (Ci)，但巢狀的資料表也包含 「 可用 」 係數 (Co)，根據下列公式計算：  
  
 F(X) = X1*C1 + X2\*C2 + ... +Xn\*Cn + X0  
  
 Activation: exp(F(X)) / (1 + exp(F(X)) )  
  
 如需詳細資訊，請參閱 [羅吉斯迴歸模型查詢範例](logistic-regression-model-query-examples.md)。  
  
## <a name="customizing-the-logistic-regression-algorithm"></a>自訂羅吉斯迴歸演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 羅吉斯迴歸演算法支援數個會影響所產生之採礦模型的行為、效能和精確度的參數。 您也可以在用於輸入的資料行上設定模型旗標，藉以修改模型的行為。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 下表描述可搭配 Microsoft 羅吉斯迴歸演算法使用的參數。  
  
 HOLDOUT_PERCENTAGE  
 指定用於計算鑑效組錯誤之定型資料內的案例百分比 HOLDOUT_PERCENTAGE 在培訓採礦模型時是做為停止準則的一部份。  
  
 預設值是 30。  
  
 HOLDOUT_SEED  
 在隨機決定鑑效組資料時，指定用來植入虛擬隨機產生器的數字。 如果 HOLDOUT_SEED 是設定為 0，則此演算法會依據採礦模型的名稱產生種子，以保證在重新處理期間模型內容保持不變。  
  
 預設值是 0。  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 定義演算法在叫用特徵選取之前，可以處理的輸入屬性數目。 將此值設定為 0 可關閉特徵選取。  
  
 預設值是 255。  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 定義演算法在叫用特徵選取之前，可以處理的輸出屬性數目。 將此值設定為 0 可關閉特徵選取。  
  
 預設值是 255。  
  
 MAXIMUM_STATES  
 指定演算法所支援之屬性狀態的最大數目。 如果屬性擁有的狀態數目大於狀態的最大數目，演算法會使用屬性最常用的狀態，並忽略其餘的狀態。  
  
 預設值為 100。  
  
 SAMPLE_SIZE  
 指定用來定型模型的案例數目。 此演算法提供者會使用此數字或不包括在鑑效組百分比 (由 HOLDOUT_PERCENTAGE 參數指定) 中的總案例數百分比，以較小者為準。  
  
 換句話說，如果 HOLDOUT_PERCENTAGE 設定為 30，則演算法將使用此參數的值，或等於總案例數 70% 的值，以較小者為準。  
  
 預設值是 10000。  
  
### <a name="modeling-flags"></a>模型旗標  
 系統支援下列模型旗標，可搭配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 羅吉斯迴歸演算法使用。  
  
 NOT NULL  
 表示資料行不能包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。  
  
 適用於採礦結構資料行。  
  
 MODEL_EXISTENCE_ONLY  
 表示資料行將被視為擁有兩個可能狀態：`Missing` 和 `Existing`。 Null 為遺漏值。  
  
 適用於採礦模型資料行。  
  
## <a name="requirements"></a>需求  
 羅吉斯迴歸模型必須包含索引鍵資料行、輸入資料行和至少一個可預測資料行。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 羅吉斯迴歸演算法支援特定輸入資料行內容類型、可預測資料行內容類型和模型旗標，這些都會在下表中列出。 如需內容類型用於採礦模型時所代表意義的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](content-types-data-mining.md)。  
  
|「資料行」|內容類型|  
|------------|-------------------|  
|輸入屬性|Continuous、Discrete、Discretized、Key、Table|  
|可預測屬性|Continuous、Discrete、Discretized|  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 羅吉斯迴歸演算法](microsoft-logistic-regression-algorithm.md)   
 [線性迴歸模型查詢範例](linear-regression-model-query-examples.md)   
 [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-logistic-regression-models.md)   
 [Microsoft 類神經網路演算法](microsoft-neural-network-algorithm.md)  
  
  
