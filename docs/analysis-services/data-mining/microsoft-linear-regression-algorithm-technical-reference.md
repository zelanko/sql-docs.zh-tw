---
title: "Microsoft 線性迴歸演算法技術參考 |Microsoft 文件"
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
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ed842a83a00412da1fce19e7519049d4171baf21
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Microsoft 線性迴歸演算法技術參考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法是 Microsoft 決策樹演算法的特殊版本，適用於連續屬性的模型配對。 本主題說明演算法的實作、描述如何自訂演算法的行為，以及提供查詢模型其他資訊的連結。  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>線性迴歸演算法的實作  
 Microsoft 決策樹演算法可用於多種工作：線性迴歸、分類或關聯分析。 若要針對線性迴歸的用途實作這個演算法，演算法的參數會受到控制，以限制樹狀結構的成長並將模型中的所有資料保存在單一節點中。 換句話說，雖然線性迴歸是以決策樹為基礎，但是此樹狀結構僅包含一個單一節點，而且沒有任何分支：所有資料都在根節點中。  
  
 若要完成此動作，演算法的 *MINIMUM_LEAF_CASES* 參數會設定為大於或等於演算法用於定型採礦模型之案例的總數。 以此方式設定參數時，演算法絕不會建立分岔，因此會執行線性迴歸。  
  
 代表迴歸線的方程式採用一般形式 y = ax + b，即所謂的迴歸方程式。 變數 Y 代表輸出變數，X 代表輸入變數，而 a 和 b 為可調整係數。 您可以藉由查詢已完成的採礦模型，擷取有關迴歸公式的係數、截距，以及其他資訊。 如需詳細資訊，請參閱 [線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)。  
  
### <a name="scoring-methods-and-feature-selection"></a>計分方法與特徵選取  
 所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦演算法都會自動使用特徵選取來改善分析並減少處理的負載。 在線性迴歸中，用於特徵選取的方法為有趣性分數，因為模型支援僅支援連續資料行。 下表顯示線性迴歸演算法與決策樹演算法的特徵選取差異，供參考之用。  
  
|演算法|分析的方法|註解|  
|---------------|------------------------|--------------|  
|線性迴歸|有趣性分數|預設值。<br /><br /> 可用於決策樹演算法的其他特徵選取方法僅適用於離散變數，因此不適用於線性迴歸模型。|  
|決策樹|有趣性分數<br /><br /> Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|如果任何資料行包含非二進位連續數值，則所有資料行都會使用有趣性分數以確保一致性。 否則，會使用預設值或指定的方法。|  
  
 針對決策樹模型控制特徵選取的演算法參數為 MAXIMUM_INPUT_ATTRIBUTES 和 MAXIMUM_OUTPUT。  
  
## <a name="customizing-the-linear-regression-algorithm"></a>自訂線性迴歸演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法支援會影響所產生之採礦模型的行為、效能和精確度的參數。 您也可以設定採礦模型資料行或採礦結構資料行上的模型旗標來控制處理資料的方式。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 下表列出針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法提供的參數。  
  
|參數|說明|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|定義演算法在叫用特徵選取之前，可以處理的輸入屬性數目。 將此值設定為 0 可關閉特徵選取。<br /><br /> 預設值是 255。|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|定義演算法在叫用特徵選取之前，可以處理的輸出屬性數目。 將此值設定為 0 可關閉特徵選取。<br /><br /> 預設值是 255。|  
|*FORCE_REGRESSOR*|強制演算法使用指定的資料行作為迴歸輸入變數，不考慮演算法計算出來之資料行的重要性。|  
  
### <a name="modeling-flags"></a>模型旗標  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法支援下列模型旗標。 當您建立採礦結構或採礦模型時，您會定義模型旗標來指定分析期間要如何處理每個資料行中的值。 如需詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)。  
  
|模型旗標|說明|  
|-------------------|-----------------|  
|NOT NULL|表示資料行不能包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。<br /><br /> 適用於採礦結構資料行。|  
|REGRESSOR|表示資料行包含分析時應視為潛在獨立變數的連續數值。 適用於採礦模型資料行。<br /><br /> 注意：為資料行加上旗標做為迴歸輸入變數無法確保將該資料行當做最終模型中的迴歸輸入變數使用。|  
  
### <a name="regressors-in-linear-regression-models"></a>線性迴歸模型中的迴歸輸入變數  
 線性迴歸模型是以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法為基礎。 不過，即使您不使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法，任何決策樹模型仍可能包含代表連續屬性迴歸的樹狀結構或節點。  
  
 您不需要指定連續的資料行代表迴歸輸入變數。 即使未在資料行上設定 REGRESSOR 旗標， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法也會將資料集分割成具備有意義之模式的區域。 其差別是當您設定模型旗標時，演算法會嘗試尋找 `a*C1 + b*C2 + ...` 形式的迴歸方程式，以在樹狀結構的節點中比對模式。 之後會計算剩餘數的總和，如果差異過大，就會在樹狀結構中強制進行分割。  
  
 例如，如果您使用 Income 作為屬性來預測客戶購買行為，且在 [Income] 資料行上設定 REGRESSOR 模型旗標，則演算法首先會使用標準迴歸公式來比對值。 如果差異過大，就會放棄迴歸公式，且根據其他的屬性分割樹狀結構。 在分割之後，決策樹演算法就會接著嘗試在每個分支中比對收入的迴歸輸入變數。  
  
 您可以使用 FORCED_REGRESSOR 參數來確保演算法會使用特定的迴歸輸入變數。 這個參數可以搭配 Microsoft 決策樹演算法及 Microsoft 線性迴歸演算法使用。  
  
## <a name="requirements"></a>需求  
 線性迴歸模型必須包含索引鍵資料行、輸入資料行和至少一個可預測資料行。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法支援下表所列的特定輸入資料行和可預測資料行。 如需內容類型用於採礦模型時所代表意義的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
|資料行|內容類型|  
|------------|-------------------|  
|輸入屬性|Continuous、Cyclical、Key、Table 和 Ordered|  
|可預測屬性|Continuous、Cyclical 和 Ordered|  
  
> [!NOTE]  
>  系統支援**Cyclical** 和 **Ordered** content types are supported, but the algorithm treats them as discrete values 和 does not perform special processing.  
  
## <a name="see-also"></a>請參閱＜  
 [Microsoft 線性迴歸演算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)   
 [線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  

