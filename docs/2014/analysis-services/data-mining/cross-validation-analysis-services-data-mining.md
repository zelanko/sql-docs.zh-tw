---
title: 交叉驗證 (Analysis Services-資料採礦) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
- scoring [data mining]
- accuracy testing [data mining]
ms.assetid: 718b9072-0f35-482a-a803-9178002ff5b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 550914167b005803e7ff39ebbcf3727f7b6b0b8c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526097"
---
# <a name="cross-validation-analysis-services---data-mining"></a>交叉驗證 (Analysis Services - 資料採礦)
  「交叉驗證」是一項標準分析工具，而且它是協助您開發並微調資料採礦模型的重要功能。 在您建立了採礦結構和相關的採礦模型之後，就可以使用交叉驗證來確定模型的有效性。  交叉驗證具有下列應用方式：  
  
-   驗證特定採礦模型的健全性。  
  
-   從單一陳述式評估多個模型。  
  
-   建立多個模型，然後根據統計資料來識別最佳模型。  
  
 本節描述如何使用針對資料採礦提供的交叉驗證功能，以及如何針對單一模型或是以單一資料集為根據的多個模型來解譯交叉驗證的結果。  
  
## <a name="overview-of-cross-validation-process"></a>交叉驗證程序的概觀  
 交叉驗證包含兩個階段：定型和產生結果。 這些階段包含下列步驟：  
  
-   選取目標採礦結構。  
  
-   指定您想要測試的模型。 這是選擇性步驟；您也可以只測試採礦結構。  
  
-   指定參數來測試定型的模型。  
  
    -   可預測的屬性、預測的值和精確度臨界值。  
  
    -   將結構或模型資料分割成的摺疊數。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所建立並定型的模型數目與摺疊數目一樣。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會針對每個模型中的每個摺疊或是整體資料集傳回一組精確度標準。  
  
## <a name="configuring-cross-validation"></a>設定交叉驗證  
 您可以自訂交叉驗證的運作方式，以便控制交叉區段的數目、測試的模型，以及預測的精確度列。 如果您使用交叉驗證預存程序，就可以同時指定用來驗證模型的資料集。 這些豐富的選項表示您可以輕易地產生許多組之後必須比較和分析的不同結果。  
  
 本節提供的資訊可協助您正確地設定交叉驗證。  
  
### <a name="setting-the-number-of-partitions"></a>設定資料分割的數目  
 當您指定資料分割的數目時，便決定了即將建立的暫時性模型數目。 對於每個資料分割而言，資料的交叉區段會標示為當做測試集使用，而且針對不在資料分割中的其餘資料所做的定型會建立新的模型。 這項程序會重複進行，直到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 已建立並測試指定的模型數目為止。 您指定要用於交叉驗證的資料會平均地分配給所有資料分割。  
  
 下圖中的範例將說明指定了三個摺疊時，資料的使用方式。  
  
 ![交叉驗證如何分割資料](../media/xvoverviewmain.gif "交叉驗證如何分割資料")  
  
 在上圖的狀況中，採礦結構包含用於測試的鑑效組資料集，但是尚未加入用於交叉驗證的測試資料集。 因此，訓練資料集中的所有資料 (採礦結構中 70% 的資料) 都會用於交叉驗證。 交叉驗證報表會顯示每個資料分割中所用的案例總數。  
  
 您也可以指定要使用的整體案例數目，藉以指定在交叉驗證期間使用的資料量。 這些案例會平均地分配給所有摺疊。  
  
 如果採礦結構儲存在 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的執行個體中，您可以針對摺疊數目設定的最大值就是 256 或案例的數目 (兩者取較小者)。 如果您要使用工作階段採礦結構，最大摺疊數目就是 10。  
  
> [!NOTE]  
>  當您增加摺疊的數目時，執行交叉驗證所需的時間就會因而增加，因為系統必須針對每個摺疊產生並測試一個模型。 如果摺疊的數目過高，您可能會遇到效能問題。  
  
### <a name="setting-the-accuracy-threshold"></a>設定精確度臨界值  
 此狀態臨界值可讓您設定預測的精確度列。 對於每個案例而言，模型會計算 *「預測機率」*(Predict Probability)，這表示預測狀態正確的機率。 如果預測機率超過精確度列，預測就會計算成正確。如果沒有超過，預測就會計算成不正確。 您可以將 [狀態臨界值] 設定為介於 0.0 與 1.0 之間的數字來控制此值，其中較接近 1 的數字代表對於預測有信心的強烈等級，而較接近 0 的數字則代表預測不太可能成真。 狀態臨界值的預測值為 NULL，表示具有最高機率的預測狀態會被視為目標值。  
  
 您應該注意，狀態臨界值的設定會影響模型精確度的量值。 例如，假設您有三個想要測試的模型。 所有模型都是根據相同的採礦結構，而且全都預測資料行 [Bike Buyer]。 此外，您也想要預測單一值 1，這表示「是的，將會購買」。 這三個模型傳回預測機率為 0.05、0.15 和 0.8 的預測。 如果您將狀態臨界值設定為 0.10，其中兩個預測就會計算成正確。 如果您將狀態臨界值設定為 0.5，只有一個模型會計算成已傳回正確的預測。 如果您使用預設值 Null，最可能的預測就會計算成正確。 在此情況中，這三個預測都會計算成正確。  
  
> [!NOTE]  
>  雖然您可以設定臨界值的值為 0.0，但是這個值沒有意義，因為每個預測都將計算成正確，即使是機率為零的預測也一樣。 請小心不要將 [狀態臨界值] 設定為 0.0。  
  
### <a name="choosing-models-and-columns-to-validate"></a>選擇要驗證的模型和資料行  
 當您使用資料採礦設計師中的 [交叉驗證] 索引標籤時，必須先從清單選取可預測的資料行。 一般而言，採礦結構可以支援許多採礦模型，但並不是所有的採礦模型都使用同一個可預測資料行。 當您執行交叉驗證時，只有使用同一個可預測資料行的模型可包含在報表中。  
  
 若要選擇可預測屬性，請按一下 [目標屬性]，然後從清單選取資料行。 如果目標屬性是巢狀資料行或巢狀資料表中的資料行，您必須輸入的巢狀使用格式的資料行名稱\<巢狀資料表名稱 > （索引鍵）。\<巢狀資料行 >。 如果從巢狀資料表所使用的唯一資料行是索引鍵資料行，您可以使用\<巢狀資料表名稱 > （索引鍵）。  
  
 在您選取可預測屬性之後， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會自動測試所有使用同一個可預測屬性的模型。 如果目標屬性包含離散的值，且您有想要預測的特定值，則可以在選取可預測資料行之後，選擇性地輸入目標狀態。  
  
 目標狀態的選擇會影響傳回的量值。 如果您指定目標屬性-也就是資料行名稱-並不會挑選您想要根據其預測最有可能的狀態來評估模型的預設值進行預測，模型的特定值。  
  
 當您搭配叢集模型使用交叉驗證時，沒有可預測的資料行；而是要從 [目標屬性] 清單方塊中的清單選取 [#Cluster]。 在選取這個選項之後，其他與叢集模型無關的選項 (例如，[目標狀態]) 就會停用。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 接著會測試所有與採礦結構相關聯的叢集模型。  
  
## <a name="tools-for-cross-validation"></a>交叉驗證工具  
 您可以從資料採礦設計師使用交叉驗證，或者藉由執行預存程序來執行交叉驗證。  
  
 如果您使用資料採礦設計師工具來執行交叉驗證，就可以在單一對話方塊中設定定型和精確度結果參數。 這樣可讓您更輕易地設定和檢視結果。 您可以測量與單一採礦結構有關之所有採礦模型的精確度，然後立即在 HTML 報表中檢視結果。 此外，預存程序會提供一些優點，例如新增的自訂內容以及為程序撰寫指令碼的功能。  
  
### <a name="cross-validation-in-data-mining-designer"></a>資料採礦設計師中的交叉驗證  
 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server Development Studio 中使用 [採礦精確度圖表] 檢視的 [交叉驗證] 索引標籤，藉以執行交叉驗證。  
  
 若要查看如何使用此使用者介面建立交叉驗證報表的範例，請參閱[建立交叉驗證報表](create-a-cross-validation-report.md)。  
  
### <a name="cross-validation-stored-procedures"></a>交叉驗證預存程序  
 對於進階使用者而言，交叉驗證也可以完全參數化系統預存程序的形式來提供。 您可以從 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 或任何 Managed 程式碼應用程式連接至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行個體，藉以執行這些預存程序。  
  
 這些預存程序是依據採礦模型類型分組的。 其中一組預存程序只會搭配叢集模型一起運作。 其他另一組預存程序則會搭配其他採礦模型一起運作。  
  
 對於每一種類型的採礦模型而言 (不論是叢集或非叢集式)，這些預存程序都會在兩個單獨的階段執行交叉驗證。  
  
 **分割資料並產生資料分割的標準**  
  
 在第一個階段中，您會呼叫系統預存程序，此程序所建立的資料分割數目與您在資料集內部指定的數目一樣，而且它會針對每個資料分割傳回精確度結果。 然後 Analysis Services 會針對每個標準計算資料分割的平均和標準差。  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining)  
  
 **產生整個資料集的標準**  
  
 在第二個階段中，您會呼叫另一組預存程序。 這些預存程序不會分割資料集，但是會針對整個指定的資料集傳回精確度結果。 如果您已經分割和處理採礦結構，您可以呼叫第二組預存程序來得到結果。  
  
-   [SystemGetAccuracyResults &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining)  
  
#### <a name="defining-the-testing-data"></a>定義測試資料  
 當您執行計算精確度的交叉驗證預存程序 (SystemGetAccuracyResults 或 SystemGetClusterAccuracyResults) 時，您可以指定在交叉驗證期間進行測試所使用的資料來源。 使用者介面中無法使用這個選項。  
  
 您可以將下列任何選項指定為測試資料來源：  
  
-   僅使用定型資料。  
  
-   包含現有的測試資料集。  
  
-   僅使用測試資料集。  
  
-   將現有的篩選套用至每個模型。  
  
-   定型集、測試集和模型篩選的任何組合。  
  
 若要指定測試資料來源，您會針對預存程序的 `DataSet` 參數提供整數值。 如需引數值的清單，請參閱相關預存程序參考主題的＜備註＞一節。  
  
 如果您使用資料採礦設計師中的 [交叉驗證] 報表來執行交叉驗證，就無法變更所使用的資料集。 根據預設，系統會使用每個模型的定型案例。 如果某個篩選與某個模型相關聯，就會套用此篩選。  
  
## <a name="results-of-cross-validation"></a>交叉驗證的結果  
 如果您使用資料採礦設計師，這些結果會顯示在類似方格的 Web 檢視器中。 如果您使用交叉驗證預存程序，這些相同的結果會以資料表形式傳回。  
  
 報表包含兩種類型的量值：在分成若干摺疊時，指示資料集變化性的彙總，以及每一個摺疊之精確度的模型特有量值。 下列主題提供有關這些量值的詳細資訊：  
  
 [交叉驗證公式](cross-validation-formulas.md)  
  
 依測試類型列出所有量值。 描述一般情況下可以解譯量值的方式。  
  
 [交叉驗證報表中的量值](measures-in-the-cross-validation-report.md)  
  
 描述用來計算每一個量值的公式，並列出可以套用每一個量值的屬性類型。  
  
## <a name="restrictions-on-cross-validation"></a>交叉驗證的限制  
 如果使用 SQL Server Development Studio 中的交叉驗證報表來執行交叉驗證，則可測試的模型及可設定的參數就會有些限制。  
  
-   根據預設，所有與選取的採礦結構相關聯的所有模型都會經過交叉驗證。 您無法指定單一模型或模型清單。  
  
-   以「Microsoft 時間序列」演算法或「Microsoft 時序叢集」演算法為基礎的模型不支援交叉驗證。  
  
-   如果採礦結構不包含任何可藉由交叉驗證而測試的模型，就無法建立報表。  
  
-   如果採礦結構同時包含叢集和非叢集模型，而您沒有選擇 **#Cluster** 選項，則兩種模型的結果都會顯示在同一報表中 (即使屬性、狀態和臨界值設定可能並不適合叢集模型)。  
  
-   某些參數值會受到限制。 例如，在摺疊數超過 10 時會顯示警告，因為產生這麼多的模型可能會導致報表顯示緩慢。  
  
 如果您要測試多個採礦模型，而且這些模型具有篩選，系統就會個別篩選每個模型。 您無法在交叉驗證期間將篩選加入至模型，或變更模型的篩選。  
  
 由於交叉驗證預設會測試與結構相關聯的所有採礦模型，因此如果某些模型具有篩選而其他沒有，您可能就會收到不一致的結果。 若要確保您只會比較這些具有相同篩選的模型，您應該使用預存程序並指定採礦模型的清單。 或者，請單獨使用沒有篩選的採礦結構測試集來確保系統會針對所有模型使用一致的資料集。  
  
 如果您使用預存程序來執行交叉驗證，您有另外一個選擇，也就是選擇測試資料的來源。 如果您使用資料採礦設計師來執行交叉驗證，您必須使用與此模型或結構相關聯的測試資料集 (如果有的話)。 一般來說，如果您想要指定進階設定，則應該使用交叉驗證預存程序。  
  
 交叉驗證無法搭配時間序列或時序叢集模型使用。 具體而言，交叉驗證無法搭配包含 KEY TIME 資料行或 KEY SEQUENCE 資料行的任何模型使用。  
  
## <a name="related-content"></a>相關內容  
 如需有關交叉驗證的詳細資訊，或是有關測試採礦模型之相關方法 (例如，精確度圖表) 的資訊，請參閱以下主題。  
  
|主題|連結|  
|------------|-----------|  
|描述如何在 SQL Server Development Studio 中設定交叉驗證參數。|[交叉驗證索引標籤 &#40;採礦精確度圖表檢視&#41;](../cross-validation-tab-mining-accuracy-chart-view.md)|  
|描述交叉驗證所提供的標準|[交叉驗證公式](cross-validation-formulas.md)|  
|說明交叉驗證報表格式，並定義針對每一個模型類型提供的統計量值。|[交叉驗證報表中的量值](measures-in-the-cross-validation-report.md)|  
|列出用來計算交叉驗證統計資料的預存程序。|[資料採礦預存程序 &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)|  
|||  
|描述如何針對採礦結構和相關模型建立測試資料集。|[定型和測試資料集](training-and-testing-data-sets.md)|  
|請參閱其他精確度圖表類型的範例。|[分類矩陣 &#40;Analysis Services - 資料採礦&#41;](classification-matrix-analysis-services-data-mining.md)<br /><br /> [增益圖 &#40;Analysis Services - 資料採礦&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [收益圖 &#40;Analysis Services - 資料採礦&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [散佈圖 &#40;Analysis Services - 資料採礦&#41;](scatter-plot-analysis-services-data-mining.md)|  
|描述建立各種精確度圖表的步驟。|[測試及驗證工作與操作方法 &#40;資料採礦&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>另請參閱  
 [測試及驗證 &#40;資料採礦&#41;](testing-and-validation-data-mining.md)  
  
  
