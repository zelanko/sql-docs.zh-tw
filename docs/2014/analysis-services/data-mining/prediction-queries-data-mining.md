---
title: 預測查詢（資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a1026597a0ae000b91e088d2457b3c9dd607044b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083121"
---
# <a name="prediction-queries-data-mining"></a>預測查詢 (資料採礦)
  典型資料採礦專案的目標是要使用採礦模型來進行預測。 例如，您可以預測特定伺服器叢集的預期停機時間，或產生分數以指出特定客戶是否可能回應廣告宣傳活動。 若要執行所有這些作業，您需要建立預測查詢。  
  
 就功能而言，SQL Server 中支援不同類型的預測查詢 (視查詢的輸入類型而定)：  
  
|查詢類型|查詢選項|  
|----------------|-------------------|  
|單一預測查詢|當您想要預測單一新案例或多個新案例的結果時，請使用單一查詢。 您可直接在查詢中提供輸入值，而查詢會當做單一工作階段執行。|  
|批次預測|當您擁有想要送入模型中的外部資料時，請使用批次預測當做預測基礎。 若要對整組資料做出預測，您會將外部來源中的資料對應到模型中的資料行，然後指定您想要輸出的預測資料類型。<br /><br /> 對整個資料集的查詢會在單一工作階段中執行，讓這個選項比傳送多個重複查詢更有效率。|  
|時間序列預測|當您想要預測某個未來步驟數的值時，請使用時間序列查詢。 SQL Server 資料採礦會在時間序列查詢中提供以下功能：<br /><br /> 您可以加入新的資料當做查詢的一部分來擴充現有的模型，然後根據複合數列做出預測。<br /><br /> 您可以使用 REPLACE_MODEL_CASES 選項將現有的模型套用至新的資料數列。<br /><br /> 您可以執行交叉預測。|  
  
 下列各節描述預測查詢的一般語法、不同預測查詢類型，以及如何使用預測查詢的結果。  
  
 [基本預測查詢設計](#bkmk_PredQuery)  
  
-   [加入預測函數](#bkmk_PredFunc)  
  
-   [單一查詢](#bkmk_SingletonQuery)  
  
-   [批次預測查詢](#bkmk_BatchQuery)  
  
 [使用查詢的結果](#bkmk_WorkResults)  
  
##  <a name="bkmk_PredQuery"></a>基本預測查詢設計  
 當您建立預測時，通常要提供一些新資料並要求模型根據新的資料產生預測。  
  
-   在批次預測查詢中，您會使用 *「預測聯結」*(Prediction Join) 將模型對應至外部資料來源。  
  
-   在單一預測查詢中，您會輸入一個或多個值當做輸入。 您可以使用單一預測查詢來建立多個預測。 但是，如果您需要建立多個預測，當您使用批次查詢時的效能會更好。  
  
 單一查詢和批次預測查詢皆使用 PREDICTION JOIN 語法定義新資料。 不同之處在於預測聯結之輸入端的指定方式。  
  
-   在批次預測查詢中，資料來自使用 OPENQUERY 語法指定的外部資料來源。  
  
-   在單一預測查詢中，資料會以內嵌方式當做查詢的一部分提供。  
  
 對於時間序列模型而言，不一定需要輸入資料；您可以只使用模型中的現有資料做出預測。 但是，如果您指定新的輸入資料，必須決定要使用新資料來更新及擴充模型，還是要取代原本在模型中使用的原始資料數列。  如需這些選項的詳細資訊，請參閱 [Time Series Model Query Examples](time-series-model-query-examples.md)。  
  
###  <a name="bkmk_PredFunc"></a>加入預測函數  
 除了預測值之外，您也可以自訂預測查詢以傳回與預測相關的各種資訊類型。 例如，如果預測建立一份建議客戶購買的產品清單，您可能也想傳回每個預測的機率，以進行排名，並只向使用者呈現熱門建議。  
  
 若要這樣做，您需要將 *「預測函數」* (Prediction Function) 加入至查詢。 每個模型或查詢類型都支援特定的函數。 例如，叢集模型支援特殊的預測函數，可針對模型建立的叢集提供額外的詳細資料，而時間序列模型則含有可計算一段時間之差異的函數。 也有可用於幾乎所有模型類型的一般預測函數。 如需不同查詢類型所支援的預測函數清單，請參閱本 DMX 參考主題：[一般預測函數 &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)。  
  
###  <a name="bkmk_SingletonQuery"></a>建立單一預測查詢  
 當您想要即時建立快速預測時，單一預測查詢便很有用。 常見的案例可能是您已經向客戶取得資訊 (或許是使用網站上的表單)，而且您想要以單一預測查詢的輸入形式提交該資料。 例如，當客戶從清單中選擇產品時，您可以使用選取內容當做預測最佳建議產品的查詢輸入。  
  
 單一預測查詢不需要包含輸入的個別資料表。 相反地，您會提供一個或多個資料列值做為模型的輸入，然後再即時傳回一個或多個預測。  
  
> [!WARNING]  
>  儘管名稱，單一預測查詢不只會進行單一預測，您可以針對每一組輸入產生多個預測。 若要提供多個輸入案例，您會針對每一個輸入案例建立 SELECT 陳述式，並將其與 UNION 運算子結合。  
  
 當您建立單一預測查詢時，必須以 PREDICTION JOIN 的形式為模型提供新資料。 這表示即使不是對應至實際的資料表，也必須確定新資料符合採礦模型中現有的資料行。 如果新資料行和新資料完全相符，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為您對應資料行。 這稱為 *NATURAL PREDICTION JOIN*。 不過，如果資料行不相符，或者新資料所包含的資料類型和數量與模型中的不同，您必須指定模型中與新資料對應的資料行，或指定遺漏的值。  
  
###  <a name="bkmk_BatchQuery"></a>批次預測查詢  
 如果您有外部資料想要用來做預測，批次預測查詢便很有用。 例如，您可能已經建立一個模型，此模型會根據客戶的線上活動和購買歷史記錄來為客戶分類。 您可將該模型套用到最新取得的潛在客戶清單，以便建立銷售預測或是辨識建議促銷活動的目標客群。  
  
 當您執行預測聯結時，必須將模型中的資料行對應到新資料來源中的資料行。 因此，您選擇當做輸入的資料來源必須包含與模型中資料類似的內容。 新資訊不必完全相符，也可以不完整。 例如，假設使用收入和年齡資訊來定型模型，但是用於預測的客戶清單有年齡資訊，卻沒有與收入有關的任何資訊。 在此情況下，您仍可以將新資料對應至模型，並可為每個客戶建立預測。 但是，如果收入是模型的重要預測因數，則資訊不完整會影響預測的品質。  
  
 若要取得最佳結果，應該在新資料和模型之間盡可能聯結相符的資料行。 不過，即使沒有相符的項目，查詢也會成功。 如果沒有聯結任何資料行，則查詢會傳回臨界預測，該預測相當於不具有 PREDICTION JOIN 子句的陳述式 `SELECT <predictable-column> FROM <model>` 。  
  
 當您成功對應所有相關的資料行之後，您會執行查詢，而且 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會根據模型內的模式來針對新資料中的每一個資料列做出預測。 您可以將結果儲存回資料來源檢視中包含外部資料的新資料表，或者可以複製和貼上資料 (如果您使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])。  
  
> [!WARNING]  
>  如果您使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的設計工具，則必須先將外部資料來源定義為資料來源檢視。  
  
 如果是使用 DMX 來建立預測聯結，則可使用 OPENQUERY、OPENROWSET 或 SHAPE 命令來指定外部資料來源。 DMX 範本中的預設資料存取方法是 OPENQUERY。 如需這些方法的相關資訊，請參閱 [&#60;來源資料查詢&#62;](/sql/dmx/source-data-query)。  
  
###  <a name="bkmk_TSQuery"></a>時間序列中的預測模型  
 時間序列模型與其他模型類型不同；您可以使用此模型的原貌來建立預測，或者可以提供新資料給模型，根據最近的趨勢更新模型和建立預測。 如果您加入新的資料，您可以指定應該使用新資料的方式。  
  
-   *擴充模型案例*表示您會將新的資料加入至時間序列模型中的現有資料數列。 從此以後，預測會以新的結合數列為根據。 如果您只想要將幾個資料點加入至現有的模型，此選項是不錯的選擇。  
  
     例如，假設您擁有的現有時間序列模型已經過去年度銷售資料的定型。 在收集數個月的新銷售資料後，您決定更新今年度的銷售預測。 您可以加入新資料並擴充模型來做出新預測，以建立更新模型的預測聯結。  
  
-   *取代模型案例*表示您會保留定型的模型，但以一組新的案例資料取代基礎案例。 當您想要將趨勢保留在模型中，但是將它套用到另一組資料時，這個選項會很有用。  
  
     例如，您的原始模型可能已經過一組包含極高銷售數量之資料的定型，而當您使用新的數列取代基礎資料 (也許是來自較少銷售數量的存放區) 時，您會保留趨勢，但是預測會從取代數列中的值開始。  
  
 不論使用的方法為何，預測一定是從原始數列的結尾開始。  
  
 如需如何在時間序列模型上建立預測聯結的詳細資訊，請參閱[時間序列模型查詢範例](time-series-model-query-examples.md)或 [PredictTimeSeries &#40;DMX&#41;](/sql/dmx/predicttimeseries-dmx)。  
  
##  <a name="bkmk_WorkResults"></a>使用預測查詢的結果  
 根據建立查詢的方式，用於儲存資料採礦預測查詢結果的選項也不相同。  
  
-   當您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中使用預測查詢產生器建立查詢時，可以將預測查詢的結果儲存至現有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源。 如需詳細資訊，請參閱 [檢視及儲存預測查詢的結果](view-and-save-the-results-of-a-prediction-query.md)。  
  
-   當您在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [查詢] 窗格中使用 DMX 建立預測查詢時，可以使用查詢輸出選項將結果儲存至檔案，或儲存至 [查詢結果] 窗格中做為文字或方格。 如需詳細資訊，請參閱[查詢與文字編輯器 &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)。  
  
-   當您使用 Integration Services 元件執行預測查詢時，這些工作可讓您使用可用的 ADO.NET 連接管理員或 OLEDB 連接管理員將結果寫入資料庫中。 如需詳細資訊，請參閱 [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)。  
  
 預測查詢的結果與關聯式資料庫查詢的結果不同，後者永遠傳回單一資料列的相關值，了解這一點很重要。 加入至查詢的每個 DMX 預測函數都會傳回本身的資料列集。 因此，當您對單一案例做出預測時，結果可能是一個預測值，以及數個包含其他詳細資料的巢狀資料表資料行。  
  
 如果您在單一查詢中結合數個函數，傳回結果會結合為階層式資料列集。 例如，假設您使用時間序列模型，以如下列 DMX 陳述式之類的查詢來預測銷售金額和銷售數量的未來值：  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 此查詢的結果有兩個資料行，每個預測數列各一個資料行，其中每一個資料列都包含有預測值的巢狀資料表：  
  
 **PredictedAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|201101|172067.11|  
  
|$TIME|Amount|  
|-----------|------------|  
|201102|363390.68|  
  
 **PredictedQty**  
  
|$TIME|數量|  
|-----------|--------------|  
|201101|77|  
  
|$TIME|數量|  
|-----------|--------------|  
|201102|260|  
  
 如果提供者無法處理階層式資料列集，則您可以在預測查詢中使用 FLATTEN 關鍵字將結果扁平化。 如需包括扁平化資料列集範例的詳細資訊，請參閱 [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;資料採礦&#41;的內容查詢](content-queries-data-mining.md)   
 [資料定義查詢 &#40;資料採礦&#41;](data-definition-queries-data-mining.md)  
  
  
