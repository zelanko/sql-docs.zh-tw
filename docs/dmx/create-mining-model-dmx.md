---
title: 建立採礦模型 (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE MINING MODEL
- CREATE
- CREATE_MINING_MODEL
dev_langs:
- DMX
helpviewer_keywords:
- RELATED TO column
- mining models [Analysis Services], creating
- column definition lists [DMX]
- parameter lists [DMX]
- SESSION clause
- CREATE MINING MODEL statement
ms.assetid: 43e4b591-7b34-494c-9b2d-7f0fe69af788
caps.latest.revision: 57
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3c4720b0ecb2dcf3aa17f250a30f106ddd1e941f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="create-mining-model-dmx"></a>CREATE MINING MODEL (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在資料庫中建立新採礦模型與採礦結構。 您可以在陳述式中定義新模型，或者使用預測模型標記語言 (PMML)，來建立模型。 第二個選項只供進階使用者使用。  
  
 採礦結構的命名方式，是在模型名稱後附加「_structure」，這可確保結構名稱與模型名稱一樣保持唯一。  
  
 若要建立現有採礦結構的採礦模型，使用[ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)陳述式。  
  
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
>  可以擷取一份目前的提供者所支援的演算法使用[DMSCHEMA_MINING_SERVICES 資料列集](../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)。 若要檢視目前執行個體中支援的演算法[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，請參閱[資料採礦屬性](../analysis-services/server-properties/data-mining-properties.md)。  
  
 *參數清單*  
 選擇性。 提供者自訂之演算法參數的逗號分隔清單。  
  
 *XML 字串*  
 (僅限進階使用)。XML 編碼的模型 (PMML)。 字串必須使用單引號 (') 括住。  
  
 **工作階段**子句可讓您建立的採礦模型，會在連接關閉或是工作階段的逾時自動從伺服器移除。**工作階段**採礦模型非常實用，因為它們不需要使用者必須為資料庫管理員，而且它們只會使用磁碟空間，只要連接為開啟。  
  
 **WITH DRILLTHROUGH**子句能夠鑽研新採礦模型。 唯有您建立模型時，才能啟用鑽研。 對於某些模型類型而言，需要鑽研才能夠在自訂檢視器中瀏覽此模型。 預測或是使用 Microsoft 一般內容樹狀檢視器來瀏覽此模型時，並不需要鑽研。  
  
 **CREATE MINING MODEL**陳述式會建立新的採礦模型為基礎的資料行定義清單、 演算法及演算法參數清單。  
  
### <a name="column-definition-list"></a>資料行定義清單  
 定義使用資料行定義清單之模型結構的方式，是包含每個資料行的下列資訊：  
  
-   名稱 (強制的)  
  
-   資料類型 (強制的)  
  
-   Distribution  
  
-   模型旗標的清單  
  
-   內容類型 (強制的)  
  
-   預測要求，指出預測這個資料行的演算法，由**預測**或**PREDICT_ONLY**子句  
  
-   關聯性的屬性資料行 （強制的只有適用），由**RELATED TO**子句  
  
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
  
-   [資料類型 &#40; 資料採礦 &#41;](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [內容類型 &#40; 資料採礦 &#41;](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [資料行散發 &#40; 資料採礦 &#41;](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [模型旗標 &#40; 資料採礦 &#41;](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 您可以在陳述式中加入子句，以描述兩個資料行之間的關聯性。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支援下列使用\<資料行關聯性 > 子句。  
  
 **與**  
 這個表單表示階層。 RELATED TO 資料行的目標可以是巢狀資料表中的索引鍵資料行、案例資料列中的分隔值資料行，或者使用 RELATED TO 子句的另一個資料行 (表示更深的階層)。  
  
 使用預測子句描述如何使用預測資料行。 下表描述兩個可能的子句。  
  
|\<預測 > 子句|描述|  
|---------------------------|-----------------|  
|**PREDICT**|這個資料行可以依模型預測，也可以在輸入案例中提供以預測其他可預測資料行的值。|  
|**PREDICT_ONLY**|這個資料行可以依模型預測，但是其值不能用於輸入案例中以預測其他可預測資料行的值。|  
  
### <a name="parameter-definition-list"></a>參數定義清單  
 您可以使用參數清單調整採礦模型的效能與功能。 參數清單的語法如下：  
  
```  
[<parameter> = <value>, <parameter> = <value>,…]  
```  
  
 如需每一種演算法相關聯的參數，請參閱[資料採礦演算法 &#40;Analysis Services-資料採礦 &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="remarks"></a>備註  
 如果您想要建立具有內建測試資料集的模型，您應該使用 CREATE MINING STRUCTURE 陳述式，後面接著 ALTER MINING STRUCTURE。 但是，並非所有模型類型都支援鑑效組資料集。 如需詳細資訊，請參閱 [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)。  
  
 如何使用 CREATEMODEL 陳述式來建立採礦模型的逐步解說，請參閱[時間序列預測 DMX 教學課程](http://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2)。  
  
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
 以下範例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯演算法建立新採礦模型。 陳述式使用資料行，以利用在模型定義中巢狀資料表的能力。 模型以修改*MINIMUM_PROBABILITY*和*MINIMUM_SUPPORT*參數。  
  
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
 以下範例使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法，透過 ARTxp 演算法建立新的採礦模型。 ReportingDate 是時間序列的索引鍵資料行，而 ModelRegion 則是資料數列的索引鍵資料行。 在這個範例中，假設資料的週期是每 12 個月。 因此， *PERIODICITY_HINT*參數設定為 12。  
  
> [!NOTE]  
>  您必須指定*PERIODICITY_HINT*使用大括號字元的參數。 此外，這個值是字串，因為它必須括在單引號:"{\<數值 >}"。  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
