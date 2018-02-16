---
title: "Microsoft 時間序列演算法技術參考 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ARTXP
- HISTORICAL_MODEL_GAP parameter
- AUTO_DETECT_PERIODICITY parameter
- time series algorithms [Analysis Services]
- ARIMA
- INSTABILITY_SENSITIVITY parameter
- PERIODICITY_HINT parameter
- MAXIMUM_SERIES_VALUE parameter
- time series [Analysis Services]
- MINIMUM_SUPPORT parameter
- HISTORIC_MODEL_COUNT parameter
- FORECAST_METHOD parameter
- MISSING_VALUE_SUBSTITUTION parameter
- MINIMUM_SERIES_VALUE parameter
- COMPLEXITY_PENALTY parameter
- PREDICTION_SMOOTHING parameter
ms.assetid: 7ab203fa-b044-47e8-b485-c8e59c091271
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 40d0c34ea4bb7e95d77ff6aa37695da4080c20ac
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="microsoft-time-series-algorithm-technical-reference"></a>Microsoft 時間序列演算法技術參考
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法包括兩種不同的演算法來分析時間序列：  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中所導入的 ARTXP 演算法是為了預測數列中的下一個可能值而最佳化。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中加入了 ARIMA 演算法來提高長期預測的精確度。  
  
 根據預設， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會個別使用每一個演算法來定型此模型，然後混合結果來針對變動數目的預測產生最佳預測。 您也可以選擇根據資料和預測需求來使用其中一個演算法。 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)]中，您也可以自訂中斷點，在預測期間控制演算法的混合。  
  
 本主題將提供有關如何實作每一個演算法以及如何自訂演算法 (藉由設定參數來微調分析和預測結果) 的詳細資訊。  
  
## <a name="implementation-of-the-microsoft-time-series-algorithm"></a>Microsoft 時間序列演算法的實作  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 研究根據 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法實作，開發 SQL Server 2005 所用的原創性 ARTXP 演算法。 因此，ARTXP 演算法可以描述為自動迴歸的樹狀模型，用以表示週期性的時間序列資料。 此演算法會將變動數目的過去項目與所預測的每一個目前項目產生關聯。 ARTXP 名稱是從自動迴歸樹狀方法 (ART 演算法) 會套用到多個未知舊狀態的事實衍生而來。 如需 ARTXP 演算法的詳細說明，請參閱 [Autoregressive Tree Models for Time-Series Analysis](http://go.microsoft.com/fwlink/?LinkId=45966)(時間序列分析的自動迴歸樹狀模型)。  
  
 SQL Server 2008 中的 Microsoft 時間序列演算法加入了 ARIMA 演算法，提高長期預測的精確度。 它是計算 Box 和 Jenkins 所描述之自動迴歸整合式移動平均程序的實作。 ARIMA 方法可用於判斷循序取得之觀察的相依性，也可以納入隨機衝擊做為模型的一部分。 ARIMA 方法也支援乘法季節分析。 建議想要深入了解 ARIMA 演算法的讀者閱讀 Box 和 Jenkins 的開創性著作；本節旨在提供有關 Microsoft 時間序列演算法如何實作 ARIMA 方法的特定詳細資料。  
  
 根據預設，Microsoft 時間序列演算法會使用 ARIMA 和 ARTXP 這兩個演算法，並混合結果以提高預測精確度。 如果您只想要使用特定方法，可以將演算法參數設定為只使用 ARTXP 或只使用 ARIMA，或者控制結合演算法結果的方式。 請注意，ARTXP 演算法支援交叉預測，但是 ARIMA 演算法則不支援。 因此，只有當您使用混合的演算法，或是當您設定此模型只能使用 ARTXP 時，才能使用交叉預測。  
  
## <a name="understanding-arima-difference-order"></a>了解 ARIMA 差分階數  
 本節介紹了解 ARIMA 模型所需的一些術語，並討論 Microsoft 時間序列演算法中的特定「差分」實作。 如需這些詞彙和概念的完整說明，建議您檢閱 Box 和 Jenkins 的著作。  
  
-   項 (term) 是數學方程式的元件。 例如，多項式方程式的項可能包含變數和常數的組合。  
  
-   Microsoft 時間序列演算法中包含的 ARIMA 公式使用「自動迴歸」和「移動平均」項。  
  
-   時間序列模型可以是「定態」或「非定態」。 「定態模型」是即使有循環也會還原為平均值的模型，而「非定態模型」則沒有均衡焦點，隨時可能會有「衝擊」(或外部變數) 所導入的更大變異或變更。  
  
-   「差分」的目標是對時間序列進行平穩化處理，讓它成為定態。  
  
-   「差分階數」代表對時間序列做值差分的次數。  
  
 Microsoft 時間序列演算法運作方式是取時間序列中的值，並嘗試將資料放入模式。 如果資料序列還不是定態，演算法就會套用差分階數。 差分階數的每個增量會嘗試讓時間序列成為定態。  
  
 例如，如果有時間序列 (z1, z2, …, zn)，並使用一階差分執行計算，會求得新序列 (y1, y2,…., yn-1)，其中 `yi = zi+1-zi`。 當差分階數是 2 時，演算法會根據衍生自第一階方程式的 y 序列，產生另一個序列 \`(x1, x2, …, xn-2)`。 正確的差分量視資料而定。 單階差分在顯示固定趨勢的模型中最常見，而二階差分則表示隨時間變動的趨勢。  
  
 根據預設，Microsoft 時間序列演算法中所用的差分階數是 -1，表示演算法會自動偵測差分階數的最佳值。 該最佳值通常是 1 (當差分為必要時)，但在某些狀況下，演算法會將該值增加為最大值 2。  
  
 Microsoft 時間序列演算法使用自動迴歸值來判斷最佳 ARIMA 差分階數。 演算法會判斷 AR 值，並設定代表 AR 項階數的隱藏參數 ARIMA_AR_ORDER。 這個隱藏參數 ARIMA_AR_ORDER 的值範圍從 -1 到 8。 在預設值 -1 時，演算法會自動選取適當的差分階數。  
  
 當 ARIMA_AR_ORDER 的值大於 1 時，演算法會將時間序列乘以多項式項。 如果多項式公式的單項解析為 1 的根或接近 1，演算法會嘗試移除該項並將差分階數增加 1，保留模型的穩定性。 如果差分階數已經是最大值，則會移除該項，而且不會變更差分階數。  
  
 例如，如果 AR 的值 = 2，產生的 AR 多項式項可能如下： `1 – 1.4B + .45B^2 = (1- .9B) (1- 0.5B)`。 請注意 `(1- .9B)` 項的根約為 0.9。 演算法會從多項式公式中消除此項，但不會將差分階數增加 1，因為它已經是最大值 2。  
  
 請務必注意， **強制** 變更差分階數的唯一方式是使用不支援的參數 ARIMA_DIFFERENCE_ORDER。 這個隱藏參數控制演算法對時間序列執行差分的次數，可藉由輸入自訂演算法參數來設定。 但除非您準備實驗並熟悉相關計算，否則不建議您變更這個值。 另請注意，目前沒有機制 (包括隱藏參數) 可讓您控制觸發差分階數增加的臨界值。  
  
 最後，請注意上述公式是簡化案例，不含季節性提示。 如果提供季節性提示，每個季節性提示的方程式左邊都要加入個別的 AR 多項式項，而且會套用相同策略來消除可能會使差分序列不穩定的項。  
  
## <a name="customizing-the-microsoft-time-series-algorithm"></a>自訂 Microsoft 時間序列演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法支援下列影響所產生之採礦模型的行為、效能及精確度的參數。  
  
> [!NOTE]  
>  Microsoft 時間序列演算法可用於所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中，但是某些進階功能 (包括自訂時間序列分析的參數) 只在特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中受支援。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 版本支援的功能](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。  
  
### <a name="detection-of-seasonality"></a>季節性的偵測  
 ARIMA 和 ARTXP 演算法支援季節性或週期性的偵測。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用快速傅立葉變換，在定型之前偵測季節性。 不過，您可以設定演算法參數來影響季節性偵測以及時間序列分析的結果。  
  
-   藉由變更 *AUTODETECT_SEASONALITY*的值，您就可以影響產生之可能時間區段的數目。  
  
-   藉由設定 *PERIODICITY_HINT*的一或多個值，您就可以為演算法提供資料中預期週期的相關資訊，以及增加偵測的精確度。  
  
> [!NOTE]  
>  ARTXP 和 ARIMA 演算法對於季節性提示非常敏感。 因此，提供錯誤的提示對於結果會有負面的影響。  
  
### <a name="choosing-an-algorithm-and-specifying-the-blend-of-algorithms"></a>選擇演算法並指定演算法的混合程度  
 根據預設，或當您選取 MIXED 選項時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會結合演算法並指派相同的權重。 但是在 Enterprise Edition 中，您可以指定特定演算法，或者您可以在結果中自訂每個演算法的比例，其方式是設定參數來加權短期或長期預測的結果。 依預設， *FORECAST_METHOD* 參數會設定為 MIXED，而 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用這兩個演算法，然後加權它們的值，讓每一個演算法的強度最大化。  
  
-   若要控制演算法的選擇，您可設定 *FORECAST_METHOD* 參數。  
  
-   如果您要使用交叉預測，您就必須使用 ARTXP 或 MIXED 選項，因為 ARIMA 不支援交叉預測。  
  
-   如果您要促進短期預測，請將 *FORECAST_METHOD* 設為 ARTXP。  
  
-   如果您要改善長期預測，請將 *FORECAST_METHOD* 設為 ARIMA。  
  
 在 Enterprise Edition 中，您也可以自訂 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 混合 ARIMA 與 ARTXP 演算法組合的方式。 您可以藉由設定 *PREDICTION_SMOOTHING* 參數來控制此混合的起點及變動率：  
  
-   如果將 *PREDICTION_SMOOTHING* 設為 0，則模型只能使用 ARTXP。  
  
-   如果將 *PREDICTION_SMOOTHING* 設為 1，則模型只能使用 ARIMA。  
  
-   如果您將 *PREDICTION_SMOOTHING* 設定為 0 與 1 之間的值，此模型會將 ARTXP 演算法加權為預測步驟的指數遞減函數。 同時，此模型也會將 ARIMA 演算法加權為與 1 互補的 ARTXP 權重。 此模型會使用正規化和穩定化常數來讓曲線平滑。  
  
 一般來說，如果您預測高達 5 個時間配量，ARTXP 幾乎都是最佳的選擇。 但是，當您增加要預測的時間配量數目時，ARIMA 的執行效能通常會比較好。  
  
 下圖說明當 *PREDICTION_SMOOTHING* 設定為預設值 0.5 時，此模型要如何混合演算法。 ARIMA 和 ARTXP 一開始會有相同的權重，但是當預測步驟的數目增加時，ARIMA 的權重就會加重。  
  
 ![混合時間序列演算法的預設曲線](../../analysis-services/data-mining/media/time-series-mixing-default.gif "混合時間序列演算法的預設曲線")  
  
 相較之下，下圖會說明當 *PREDICTION_SMOOTHING* 設定為 0.2 時，要如何混合演算法。 如果是 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]步驟，此模型會將 ARIMA 加權為 0.2，並將 ARTXP 加權為 0.8。 因此，ARIMA 的權重會以指數方式增加，ARTXP 的權重則會以指數方式減少。  
  
 ![混合時間序列模型的衰變曲線](../../analysis-services/data-mining/media/time-series-blending-curve.gif "混合時間序列模型的衰變曲線")  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 下表描述可用於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法的參數。  
  
|參數|說明|  
|---------------|-----------------|  
|*AUTO_DETECT_PERIODICITY*|指定 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 和 1 之間的數值，用於偵測週期性。 預設值為 0.6。<br /><br /> 如果將此值設定為越接近 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]，則只會偵測到週期性很強的資料。<br /><br /> 將這個值設定為越接近 1，就會探索更多接近週期性的模式，並自動產生週期性提示。<br /><br /> 注意：處理大量週期性提示時，可能會造成更長的模型定型時間及更精確的模型。|  
|*COMPLEXITY_PENALTY*|控制決策樹的成長。 預設值是 0.1。<br /><br /> 減少此值可增加分割的機率。 增加此值可減少分割的機率。<br /><br /> 注意：只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用這個參數。|  
|*FORECAST_METHOD*|指定要使用哪一個演算法來分析和預測。 可能的值為 ARTXP、ARIMA 或 MIXED。 預設值為 MIXED。|  
|*HISTORIC_MODEL_COUNT*|指定要建立的記錄模型數目。 預設值是 1。<br /><br /> 注意：只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用這個參數。|  
|*HISTORICAL_MODEL_GAP*|指定兩個連續記錄模型之間的時間延遲。 預設值是 10。 此值代表時間單位數，此單位是由模型所定義。<br /><br /> 例如，將此值設定為 g，會造成要建立記錄模型的資料，依 g、2*g、3\*g 等等的間隔而遭到時間配量截斷。<br /><br /> 注意：只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用這個參數。|  
|*INSTABILITY_SENSITIVITY*|控制預測變異數超出某個臨界值的那個點，在那個點之後，ARTXP 演算法會隱藏預測。 預設值是 1。<br /><br /> 注意：這個參數不適用於只使用 ARIMA 的模型。<br /><br /> 預設值 1 會提供與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中相同的行為。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會監視每一個預測的正規化標準差。 一旦任何預測的這個值超出臨界值，時間序列演算法就會傳回 NULL，並停止預測程序。<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 值會停止不穩定的偵測。 這表示，您可以建立無限的預測數，不論變異數為何。<br /><br /> 注意：這個參數只能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 中修改。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard 中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 只會使用預設值 1。|  
|*MAXIMUM_SERIES_VALUE*|指定用於預測的最大值。 這個參數會與 *MINIMUM_SERIES_VALUE*一起使用，將預測限制為某個預期的範圍。 例如，您可以指定任何一天的預期銷售數量絕對不能超過存貨產品數。<br /><br /> 注意：只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用這個參數。|  
|*MINIMUM_SERIES_VALUE*|指定可以預測的最小值。 這個參數會與 *MAXIMUM_SERIES_VALUE*一起使用，將預測限制為某個預期的範圍。 例如，您可以指定預期銷售數量絕對不能是負數。<br /><br /> 注意：只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用這個參數。|  
|*MINIMUM_SUPPORT*|指定要在每一個時間序列樹中產生分割所需之時間配量的最小數目。 預設值是 10。|  
|*MISSING_VALUE_SUBSTITUTION*|指定如何填滿歷程記錄資料中的間距。 根據預設，資料中不允許有間隔。 下表列出此參數的可能值：<br /><br /> **Previous**：重複先前時間配量中的值。<br /><br /> **Mean**：使用定型中使用之時間配量的移動平均。<br /><br /> 數值常數：使用指定的數目來取代所有遺漏的值。<br /><br /> **None**：預設值。 使用沿著定型模型曲線所繪製的值來取代遺漏的值。<br /><br /> <br /><br /> 請注意，如果資料包含多個數列，數列不能有不完全的邊緣。 也就是說，所有的數列都應該有相同的起點和終點。 <br />                    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 當您在時間序列模型上執行 **PREDICTION JOIN** 時，也會使用這個參數值來填滿新資料中的間距。|  
|*PERIODICITY_HINT*|提供演算法關於資料週期性的提示。 例如，若每年銷售不同，而且數列中的度量單位是月，則週期性是 12。 此參數採用 {n [, n]} 的格式，其中 n 為任意正數。<br /><br /> 方括弧 [] 內的 n 是選擇性的，可以視需要而重複。 例如，若要針對每個月提供的資料來提供多個週期性提示，您可輸入 {12, 3, 1} 來偵測年、季和月的模式。 但是，週期性對於模型的品質有很大的影響。 如果您所給的提示與實際週期性不同，對結果會有負面影響。<br /><br /> 預設值是 {1}。<br /><br /> 請注意，必須用大括號括住。 而且，這個參數具有字串資料類型。 因此，如果您在資料採礦延伸模組 (DMX) 陳述式中輸入這個參數，您必須以引號括住數字和大括號。|  
|*PREDICTION_SMOOTHING*|指定應該如何混合模型來讓預測最佳化。 您可以輸入 [!INCLUDE[tabValue](../../includes/tabvalue-md.md)] 與 1 之間的任何值，或是使用下列其中一個值：<br /><br /> [!INCLUDE[tabValue](../../includes/tabvalue-md.md)]:<br />                          指定預測只能使用 ARTXP。 已針對較少的預測數而最佳化預測。<br /><br /> 1：指定預測只能使用 ARIMA。 已針對許多的預測數而最佳化預測。<br /><br /> 0.5：預設值。 指定在預測時，這兩個演算法都應該使用，而且應該混合結果。<br /><br /> <br /><br /> 在執行預測平滑化時，使用 *FORECAST_METHOD* 參數來控制定型。   請注意，只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用這個參數。|  
  
### <a name="modeling-flags"></a>模型旗標  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法支援下列模型旗標。 當您建立採礦結構或採礦模型時，您會定義模型旗標來指定分析期間要如何處理每個資料行中的值。 如需詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)。  
  
|模型旗標|說明|  
|-------------------|-----------------|  
|NOT NULL|表示資料行不能包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。<br /><br /> 適用於採礦結構資料行。|  
|MODEL_EXISTENCE_ONLY|表示資料行將被視為擁有兩個可能狀態：「遺漏」和「現有」。 Null 為遺漏值。<br /><br /> 適用於採礦模型資料行。|  
  
## <a name="requirements"></a>需求  
 時間序列模型必須包含 Key Time 資料行，此資料行中包含唯一的值、輸入資料行和至少一個可預測資料行。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法支援特定輸入資料行內容類型、可預測資料行內容類型和模型旗標，這些都會在下表中列出。  
  
|資料行|內容類型|  
|------------|-------------------|  
|輸入屬性|Continuous、Key、Key Time 和 Table|  
|可預測屬性|Continuous、Table|  
  
> [!NOTE]  
>  系統支援 Cyclical 和 Ordered 內容類型，但是演算法將它們視為離散值，因此不會執行特殊處理。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時間序列演算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [時間序列模型查詢範例](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [時間序列模型 &#40; 的採礦模型內容Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)  
  
  
