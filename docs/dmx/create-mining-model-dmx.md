---
description: CREATE MINING MODEL (DMX)
title: 建立 (DMX) 的採礦模型 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 35382c7d1d7301d35d8517b62bac352a4ae9fb47
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726291"
---
# <a name="create-mining-model-dmx"></a>CREATE MINING MODEL (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  在資料庫中建立新採礦模型與採礦結構。 您可以在陳述式中定義新模型，或者使用預測模型標記語言 (PMML)，來建立模型。 第二個選項只供進階使用者使用。  
  
 採礦結構的命名方式，是在模型名稱後附加「_structure」，這可確保結構名稱與模型名稱一樣保持唯一。  
  
 若要建立現有的採礦結構的採礦模型，請使用 [ALTER 採礦結構 &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) 語句。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE [SESSION] MINING MODEL <model>  
(  
    [(<column definition list>)]  
)  
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH]  
CREATE MINING MODEL <model> FROM PMML <xml string>  
```  
  
## <a name="arguments"></a>引數  
 *model*  
 模型的唯一名稱。  
  
 *資料行定義清單*  
 資料行定義的逗號分隔清單。  
  
 *演算法*  
 目前提供者所定義之資料採礦演算法的名稱。  
  
> [!NOTE]  
>  您可以使用 DMSCHEMA_MINING_SERVICES 資料列 [集](/previous-versions/sql/sql-server-2012/ms126251(v=sql.110))來抓取目前提供者所支援的演算法清單。 若要查看目前實例所支援的演算法 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，請參閱 [資料採礦屬性](/analysis-services/server-properties/data-mining-properties)。  
  
 *參數清單*  
 選擇性。 提供者自訂之演算法參數的逗號分隔清單。  
  
 *XML 字串*  
  (僅供 advanced 使用。 ) XML 編碼的模型 (PMML) 。 字串必須使用單引號 (') 括住。  
  
 **Session**子句可讓您建立在連接關閉或會話超時時，自動從伺服器移除的採礦模型。**會話**採礦模型很有用，因為它們不需要使用者是資料庫管理員，而且只要開啟連接，就只會使用磁碟空間。  
  
 **WITH 鑽取**子句可讓您深入瞭解新的採礦模型。 唯有您建立模型時，才能啟用鑽研。 對於某些模型類型而言，需要鑽研才能夠在自訂檢視器中瀏覽此模型。 預測或是使用 Microsoft 一般內容樹狀檢視器來瀏覽此模型時，並不需要鑽研。  
  
 **CREATE CREATE model**語句會根據資料行定義清單、演算法和演算法參數清單，建立新的採礦模型。  
  
### <a name="column-definition-list"></a>資料行定義清單  
 定義使用資料行定義清單之模型結構的方式，是包含每個資料行的下列資訊：  
  
-   名稱 (強制的)  
  
-   資料類型 (強制的)  
  
-   散發  
  
-   模型旗標的清單  
  
-   內容類型 (強制的)  
  
-   預測要求，表示演算法預測這個資料行，由 **predict** 或 **PREDICT_ONLY** 子句表示  
  
-   屬性資料行的關聯性 (只有在套用) （由 **相關的 to** 子句表示）時，才會強制套用  
  
 使用下列資料行定義清單的語法，以定義單一資料行：  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 使用下列資料行定義清單的語法，以定義巢狀資料表資料行：  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 除了模型旗標之外，您不能從特定群組使用一個以上的子句來定義資料行。 您可以為一個資料行定義多個模型旗標。  
  
 如需可用於定義資料行之資料類型、內容類型、資料行散發及模型旗標的清單，請參閱下列主題：  
  
-   [資料類型 &#40;資料採礦&#41;](/analysis-services/data-mining/data-types-data-mining)  
  
-   [內容類型 &#40;資料採礦&#41;](/analysis-services/data-mining/content-types-data-mining)  
  
-   [資料行分佈 &#40;資料採礦&#41;](/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [模型旗標 &#40;資料採礦&#41;](/analysis-services/data-mining/modeling-flags-data-mining)  
  
 您可以在陳述式中加入子句，以描述兩個資料行之間的關聯性。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援使用下列 \<Column relationship> 子句。  
  
 **相關**  
 這個表單表示階層。 RELATED TO 資料行的目標可以是巢狀資料表中的索引鍵資料行、案例資料列中的分隔值資料行，或者使用 RELATED TO 子句的另一個資料行 (表示更深的階層)。  
  
 使用預測子句描述如何使用預測資料行。 下表描述兩個可能的子句。  
  
|\<prediction> 子句|描述|  
|---------------------------|-----------------|  
|**PREDICT**|這個資料行可以依模型預測，也可以在輸入案例中提供以預測其他可預測資料行的值。|  
|**PREDICT_ONLY**|這個資料行可以依模型預測，但是其值不能用於輸入案例中以預測其他可預測資料行的值。|  
  
### <a name="parameter-definition-list"></a>參數定義清單  
 您可以使用參數清單調整採礦模型的效能與功能。 參數清單的語法如下：  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
 如需與每個演算法相關聯的參數清單，請參閱 [資料採礦演算法 &#40;Analysis Services 資料採礦&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)。  
  
## <a name="remarks"></a>備註  
 如果您想要建立具有內建測試資料集的模型，您應該使用 CREATE MINING STRUCTURE 陳述式，後面接著 ALTER MINING STRUCTURE。 但是，並非所有模型類型都支援鑑效組資料集。 如需詳細資訊，請參閱 [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)。  
  
 如需如何使用 CREATEMODEL 語句來建立採礦模型的逐步解說，請參閱 [時間序列預測 DMX 教學](/previous-versions/sql/sql-server-2016/cc879270(v=sql.130))課程。  
  
## <a name="naive-bayes-example"></a>貝氏機率分類範例  
 以下範例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏機率分類演算法建立新的採礦模型。 Bike Buyer 資料行定義為可預測屬性。  
  
```  
CREATE MINING MODEL [NBSample]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE PREDICT  
)  
USING Microsoft_Naive_Bayes  
```  
  
## <a name="association-model-example"></a>關聯模型範例  
 以下範例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯演算法建立新採礦模型。 陳述式使用資料行，以利用在模型定義中巢狀資料表的能力。 您可以使用 *MINIMUM_PROBABILITY* 和 *MINIMUM_SUPPORT* 參數來修改模型。  
  
```  
CREATE MINING MODEL MyAssociationModel (  
    OrderNumber TEXT KEY,  
    [Products] TABLE PREDICT (  
        [Model] TEXT KEY  
    )  
)  
USING Microsoft_Association_Rules (Minimum_Probability = 0.1, MINIMUM_SUPPORT = 0.01)  
```  
  
## <a name="sequence-clustering-example"></a>時序群集範例  
 以下範例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序群集演算法建立新的採礦模型。 使用兩個索引鍵來定義模型。 OrderNumber 資料行會當做案例索引鍵使用，並指定個別訂單。 LineNumber 資料行會當做巢狀資料表索引鍵使用，並指定將項目加入訂單的順序。  
  
```  
CREATE MINING MODEL BuyingSequence (  
    [Order Number] TEXT KEY,  
    [Products] TABLE   
     (  
        [Line Number] LONG KEY SEQUENCE,  
        [Model] TEXT DISCRETE PREDICT  
    )  
)  
USING Microsoft_Sequence_Clustering  
```  
  
## <a name="time-series-example"></a>時間序列範例  
 以下範例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法，透過 ARTxp 演算法建立新的採礦模型。 ReportingDate 是時間序列的索引鍵資料行，而 ModelRegion 則是資料數列的索引鍵資料行。 在這個範例中，假設資料的週期是每 12 個月。 因此， *PERIODICITY_HINT* 參數會設定為12。  
  
> [!NOTE]  
>  您必須使用大括弧字元來指定 *PERIODICITY_HINT* 參數。 此外，因為此值為字串，所以必須以單引號括住： "{ \<numeric value> }"。  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
