---
title: 特徵選取 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], feature selections
- attributes [data mining]
- feature selection algorithms [Analysis Services]
- data mining [Analysis Services], feature selections
- neural network algorithms [Analysis Services]
- naive bayes algorithms [Analysis Services]
- decision tree algorithms [Analysis Services]
- datasets [Analysis Services]
- clustering algorithms [Analysis Services]
- coding [Data Mining]
ms.assetid: b044e785-4875-45ab-8ae4-cd3b4e3033bb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6618a4a0818519ba4c3f0bbd63a46e02b4217296
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360140"
---
# <a name="feature-selection-data-mining"></a>特徵選取 (資料採礦)
  *特徵選取*指的是常用於資料採礦，以描述的工具和技術可供輸入降低至可管理的大小，用於處理和分析。 特徵選取隱含不僅*基數減少*，這表示強加任意或預先定義的截止，可以在建立模型，但也屬性，這表示的選擇時考量的屬性數目分析師或模型化工具主動選取或捨棄屬性根據對分析的實用性。  
  
 能夠套用特徵選取對有效分析而言很重要，因為資料集經常包含比建立模型所需還要更多的資訊。 例如，資料集可能包含 500 個資料行來描述客戶的特性，但是如果其中一些資料行的資料很疏鬆，將資料加入至模型所能獲得的效益將非常有限。 如果您在建立此模型時保留不需要的資料行，定型程序期間就會需要更多 CPU 和記憶體，而且完成的模型需要更多儲存空間。  
  
 即使資源不是問題，您通常也會想要移除不需要的資料行，因為它們可能會降低已探索模式的品質，原因如下：  
  
-   某些資料行是累贅或多餘的。 這種情況會使有意義的資料模式更難發現。  
  
-   若要發現高品質的模式，大部分的資料採礦演算法需要高維度資料集提供大得多的訓練資料集。 但在某些資料採礦應用程式中，定型資料的量非常少。  
  
 如果資料來源的 500 個資料行中只有 50 個資料行的資訊對建立模型有用，您可以不將其納入模型，或使用特徵選取技術自動探索最佳的特徵，並排除統計上不重要的值。 特徵選取有助於解決兩個問題：低價值資料過多，或高價值資料過少。  
  
## <a name="feature-selection-in-analysis-services-data-mining"></a>Analysis Services 資料採礦中的特徵選取  
 特徵選取通常會在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中自動執行，且每個演算法具有一組預設的技術，可以有智慧地套用特徵減少。 特徵選取一定會在定型模型之前執行，可自動從資料集裡選擇最有可能在模型中使用的屬性。 但是，您也可以手動設定參數以影響特徵選取行為。  
  
 一般而言，特徵選取的運作方式是計算每個屬性的分數，然後僅選取擁有最佳分數的屬性。 您也可以調整高分的臨界值。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供多種可用於計算這些分數的方法，而實際套用至任何模型的方法則取決於下列因素：  
  
-   模型中所使用的演算法  
  
-   屬性的資料類型  
  
-   您可能在模型上設定的任何參數  
  
 特徵選取會套用到輸入、可預測的屬性或是資料行中的狀態。 完成特徵選取的計分之後，只有演算法選取的屬性和狀態會包含在模型建立程序中，而且可以用來預測。 如果您選擇的可預測屬性不符合特徵選取的臨界值，屬性仍可用於預測，但預測只會以模型中存在的全域統計資料為基礎。  
  
> [!NOTE]  
>  特徵選取只會影響用於模型的資料行，對採礦結構的儲存不會有任何影響。 排除在採礦模型外的資料行仍可用於結構，而採礦結構資料行中的資料則會存入快取。  
  
### <a name="definition-of-feature-selection-methods"></a>特徵選取方法的定義  
 依據您所使用的資料類型以及選擇用來分析的演算法而定，實作特徵選取的方法有許多種。 SQL Server Analysis Services 提供數種常見且妥善建立的方法來為屬性評分。 在任何演算法或資料集中所套用的方法取決於資料類型及資料行的使用方式。  
  
 「有趣性」(Interestingness) 分數是用來在包含非二進位連續數值資料的資料行中排名及排序屬性。  
  
 包含離散和離散化資料的資料行使用「Shannon 熵」(Shannon's Entropy) 和兩個貝氏 (Bayesian) 分數。 但是，如果模型包含任何連續資料行，則會使用有趣性分數評估所有輸入資料行，以確保一致性。  
  
 下一節將描述每個特徵選取方法。  
  
#### <a name="interestingness-score"></a>有趣性分數  
 如果特徵能告訴您一些有用的資訊，就具備「有趣性」。 有用的定義會因案例而異，因為資料採礦業界已開發各種方式來測量*有趣性*。 例如，*新奇*可能很有趣極端值偵測，但能夠區別密切相關的項目，或*稱為 「 辨識權重*，可能更有趣的分類。  
  
 使用 SQL Server Analysis Services 中的 「 有趣 」 的量值*熵為基礎*，這表示具有隨機散發的屬性具有較高的熵和較低的資訊優勢，因此，這類屬性會是小於有趣的。 任何特定屬性的熵都會與所有其他屬性的熵進行比較，如下所示：  
  
 Interestingness(Attribute) = - (m - Entropy(Attribute)) * (m - Entropy(Attribute))  
  
 中間熵 (或稱 m) 代表整個功能集的熵。 藉由從中間熵減去目標屬性的熵，您可以評估屬性所提供的資訊量。  
  
 每當資料行包含非二進位的連續數值資料時，依預設就會使用此分數。  
  
#### <a name="shannons-entropy"></a>Shannon 熵  
 Shannon 熵可針對特定結果而測量隨機變數的不確定性。 例如，擲銅板的熵可以表示為銅板呈現大頭的機率函數。  
  
 Analysis Services 使用下列公式來計算 Shannon 熵：  
  
 H(X) = -∑ P(xi) log(P(xi))  
  
 這個計分方法可用於分隔和離散化的屬性。  
  
#### <a name="bayesian-with-k2-prior"></a>使用 K2 優先的貝氏  
 Analysis Services 提供兩種以貝氏網路為基礎的特徵選取分數。 貝氏網路是狀態及狀態間轉換的「導向」或「非循環」圖表，代表某些狀態一定會在目前的狀態之前、某些狀態會在之後，而圖表並不會重複或迴圈。 依照定義，貝氏網路可以使用先前的知識。 不過，在計算稍後狀態的機率時要使用什麼先前狀態的問題，對於演算法的設計、效能和精確度都很重要。  
  
 貝氏網路學習的 K2 演算法是由 Cooper 和 Herskovits 所開發，常用於資料採礦中。 這個演算法可以擴充，而且可以分析多個變數，但需要對當做輸入的變數進行排序。 如需詳細資訊，請參閱 Chickering、Geiger 和 Heckerman 所著的 [Learning Bayesian Networks](https://go.microsoft.com/fwlink/?LinkId=105885) (學習貝氏網路)。  
  
 這個計分方法可用於分隔和離散化的屬性。  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>使用統一優先的貝氏狄氏等價  
 貝氏狄氏等價 (Bayesian Dirichlet Equivalent，BDE) 分數也會使用貝氏分析來評估具有資料集的網路。 BDE 計分方法是由 Heckerman 開發，以 Cooper 和 Herskovits 所開發的 BD 標準為基礎。 Dirichlet 散發是多維度散發，描述網路中每個變數的條件式機率，而且具有許多對學習有用的屬性。  
  
 使用統一優先的貝氏狄氏等價 (Bayesian Dirichlet Equivalent with Uniform Prior，BDEU) 方法假設狄氏散發的特殊案例，其中會使用數學常數來建立先前狀態的固定或統一散發。 BDE 分數也假設可能性相等，這代表不能預期資料會區別相等的結構。 換句話說，如果「If A Then B」的分數與「If B Then A」的分數相同，則不能根據資料區分結構，也不能推斷因果關係。  
  
 如需貝氏網路以及實作這些計分方法的詳細資訊，請參閱 [Learning Bayesian Networks](https://go.microsoft.com/fwlink/?LinkId=105885)(學習貝氏網路)。  
  
### <a name="feature-selection-methods-used-by-analysis-services-algorithms"></a>Analysis Services 演算法所使用的特徵選取方法  
 下表列出支援特徵選取的演算法、演算法所使用的特徵選取方法，以及設定來控制特徵選取行為的參數：  
  
|演算法|分析的方法|註解|  
|---------------|------------------------|--------------|  
|貝氏機率分類|Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|Microsoft 貝氏機率分類演算法只接受分隔或離散化的屬性，因此無法使用有趣性分數。<br /><br /> 如需這個演算法的詳細資訊，請參閱 [Microsoft 貝氏機率分類演算法技術參考](microsoft-naive-bayes-algorithm-technical-reference.md)。|  
|決策樹|有趣性分數<br /><br /> Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|如果任何資料行包含非二進位連續數值，則所有資料行都會使用有趣性分數以確保一致性。 否則，便會使用預設特徵選取方法，或是當您建立模型時所指定的方法。<br /><br /> 如需這個演算法的詳細資訊，請參閱 [Microsoft 決策樹演算法技術參考](microsoft-decision-trees-algorithm-technical-reference.md)。|  
|類神經網路|有趣性分數<br /><br /> Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|Microsoft 類神經網路演算法可以使用貝氏和以熵為基礎的方法，只要資料包含連續資料行即可。<br /><br /> 如需這個演算法的詳細資訊，請參閱 [Microsoft 類神經網路演算法技術參考](microsoft-neural-network-algorithm-technical-reference.md)。|  
|羅吉斯迴歸|有趣性分數<br /><br /> Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|雖然 Microsoft 羅吉斯迴歸演算法是根據 Microsoft 類神經網路演算法，但是您無法自訂羅吉斯迴歸模型來控制特徵選取行為。因此，特徵選取一定會預設為最適合屬性的方法。<br /><br /> 如果所有屬性都是離散或離散化的，則預設值為 BDEU。<br /><br /> 如需這個演算法的詳細資訊，請參閱 [Microsoft 羅吉斯迴歸演算法技術參考](microsoft-logistic-regression-algorithm-technical-reference.md)。|  
|群集|有趣性分數|Microsoft 群集演算法可以使用離散或離散化資料。 但是，由於每一個屬性的分數都會計算為距離，並表示為連續的數字，因此必須使用有趣性分數。<br /><br /> 如需這個演算法的詳細資訊，請參閱 [Microsoft 群集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)。|  
|線性迴歸|有趣性分數|Microsoft 線性迴歸演算法只能使用有趣性分數，因為它只支援連續的資料行。<br /><br /> 如需這個演算法的詳細資訊，請參閱 [Microsoft 線性迴歸演算法技術參考](microsoft-linear-regression-algorithm-technical-reference.md)。|  
|關聯規則<br /><br /> 時序群集|未使用|不會使用這些演算法叫用特徵選取。<br /><br /> 不過，您可以藉由設定 MINIMUM_SUPPORT 和 MINIMUM_PROBABILIITY 參數的值，控制演算法的行為，並在必要時減少輸入資料的大小。<br /><br /> 如需詳細資訊，請參閱 [Microsoft 關聯分析演算法技術參考](microsoft-association-algorithm-technical-reference.md) 和 [Microsoft 時序群集演算法技術參考](microsoft-sequence-clustering-algorithm-technical-reference.md)。|  
|時間序列|未使用|特徵選取不適用於時間序列模型。<br /><br /> 如需這個演算法的詳細資訊，請參閱 [Microsoft 時間序列演算法技術參考](microsoft-time-series-algorithm-technical-reference.md)。|  
  
## <a name="feature-selection-parameters"></a>特徵選取參數  
 在支援特徵選取的演算法中，您可以使用下列參數來控制何時開啟特徵選取。 每個演算法都具有所允許之輸入數目的預設值，但是您可以覆寫這個預設值並指定屬性的數目。 本節列出為管理特徵選取所提供的參數。  
  
#### <a name="maximuminputattributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 如果模型包含的資料行比在 *MAXIMUM_INPUT_ATTRIBUTES* 參數中所指定的數目多，則演算法會忽略認為不重要的任何資料行。  
  
#### <a name="maximumoutputattributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 同樣地，如果模型包含的可預測資料行比在 *MAXIMUM_OUTPUT_ATTRIBUTES* 參數中所指定的數目多，則演算法會忽略認為不重要的任何資料行。  
  
#### <a name="maximumstates"></a>MAXIMUM_STATES  
 如果模型包含的案例比在 *MAXIMUM_STATES* 參數中所指定的數目多，則會將最不常用的狀態群組在一起，並視為遺漏。 如果其中有任何參數設定為 0，特徵選取就會關閉，且會影響處理時間和效能。  
  
 除了這些特徵選取方法之外，您也可以透過在模型上設定「模型旗標」，或透過在結構上設定「散發旗標」，來改進演算法識別或提升有意義屬性的能力。 如需這些概念的詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](modeling-flags-data-mining.md) 和[資料行散發 &#40;資料採礦&#41;](column-distributions-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [自訂採礦模型和結構](customize-mining-models-and-structure.md)  
  
  
