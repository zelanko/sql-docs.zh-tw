---
title: "建立採礦結構 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MINING_STRUCTURE
- CREATE MINING STRUCTURE
dev_langs:
- DMX
helpviewer_keywords:
- CREATE MINING STRUCTURE statement
- mining structures [DMX], creating
- RELATED TO column
ms.assetid: c0dec39c-e90f-4afd-aeaf-a9c3e1d1a5e0
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cb0b52cf7ac2b866119ff75bbd0d7e8da8cbac84
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="create-mining-structure-dmx"></a>CREATE MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在資料庫中建立新的採礦結構，並選擇性地定義培訓和測試資料分割。 在建立採礦結構之後，您可以使用[ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)陳述式，將模型加入採礦結構。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE [SESSION] MINING STRUCTURE <structure>  
(  
    [(<column definition list>)]  
)  
[WITH HOLDOUT (<holdout-specifier> [OR <holdout-specifier>])]  
[REPEATABLE(<holdout seed>)]  
<holdout-specifier>::=  <holdout-maxpercent> PERCENT | <holdout-maxcases> CASES  
```  
  
## <a name="arguments"></a>引數  
 *結構*  
 結構的唯一名稱。  
  
 *資料行定義清單*  
 資料行定義的逗號分隔清單。  
  
 *鑑效組 maxpercent*  
 介於 1 和 100 之間的整數，表示保留給測試之用的資料百分比。  
  
 *鑑效組 maxcases*  
 表示用於測試之案例數目上限的整數。  
  
 如果為最大案例數指定的值大於輸入案例的數目，所有輸入案例都會用於測試，並且將會引發警告。  
  
> [!NOTE]  
>  如果同時指定案例的百分比和最大數目，則會使用兩個限制中的較小者。  
  
 *鑑效組種子*  
 當做種子使用以開始分割資料的整數。  
  
 如果設為 0，就會使用採礦結構識別碼的雜湊當做種子。  
  
> [!NOTE]  
>  如果您需要確認可以重新產生資料分割，您應該指定一個種子。  
  
 預設值：REPEATABLE(0)  
  
## <a name="remarks"></a>備註  
 定義採礦結構的方法是指定資料行的清單、選擇性地指定資料行之間的階層式關聯性，然後選擇性地將採礦結構分割為培訓和測試資料集。  
  
 選擇性的 SESSION 關鍵字表示此結構是暫時性結構，您僅能用於目前工作階段的持續時間。 當工作階段結束時，將會刪除此結構以及所有以此結構為基礎的模型。 若要建立暫時性採礦結構和模型，您必須先設定資料庫的 AllowSessionMiningModels 屬性。 如需詳細資訊，請參閱 [資料採礦屬性](../analysis-services/server-properties/data-mining-properties.md)。  
  
## <a name="column-definition-list"></a>資料行定義清單  
 您可以在資料行定義清單中包含每個資料行的下列資訊，以定義採礦結構：  
  
-   名稱 (強制的)  
  
-   資料類型 (強制的)  
  
-   Distribution  
  
-   模型旗標的清單  
  
-   內容類型 (強制的)  
  
-   屬性資料行的關聯性 (只有適用時才是強制的)，由 RELATED TO 子句指出  
  
 使用下列資料行定義清單的語法來定義單一資料行：  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<column relationship>]  
```  
  
 使用下列資料行定義清單的語法，以定義巢狀資料表資料行：  
  
```  
<column name>    TABLE    ( <column definition list> )  
```  
  
 如需可用於定義結構資料行之資料類型、內容類型、資料行散發，以及模型旗標的清單，請參閱下列主題：  
  
-   [資料類型 &#40; 資料採礦 &#41;](../analysis-services/data-mining/data-types-data-mining.md)  
  
-   [內容類型 &#40; 資料採礦 &#41;](../analysis-services/data-mining/content-types-data-mining.md)  
  
-   [資料行散發 &#40; 資料採礦 &#41;](../analysis-services/data-mining/column-distributions-data-mining.md)  
  
-   [模型旗標 &#40; 資料採礦 &#41;](../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
 您可以為一個資料行定義多個模型旗標值。 不過，對於一個資料行，您僅能擁有一個內容類型和一個資料類型。  
  
### <a name="column-relationships"></a>資料行關聯性  
 您可以在任何資料行定義陳述式中加入子句，以描述兩個資料行之間的關聯性。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支援下列使用\<資料行關聯性 > 子句。  
  
 **與**  
 表示階層。 RELATED TO 資料行的目標可以是巢狀資料表中的索引鍵資料行、案例資料列中的分隔值資料行，或者使用 RELATED TO 子句的另一個資料行 (表示更深的階層)。  
  
## <a name="holdout-parameters"></a>鑑效組參數  
 當您指定鑑效組參數時，您可以建立結構資料的資料分割。 您為鑑效組所指定的數量會保留給測試之用，而剩餘的資料則用於培訓。 根據預設，如果您使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 建立採礦結構，系統會為您建立鑑效組資料分割，其中包含 30% 的測試資料以及 70% 的培訓資料。 如需詳細資訊，請參閱 [Training and Testing Data Sets](../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
 如果您使用資料採礦延伸模組 (DMX) 建立採礦結構，您必須手動指定要建立的鑑效組資料分割。  
  
> [!NOTE]  
>  **ALTER MINING STRUCTURE**陳述式不支援鑑效組。  
  
 您最多可以指定三個鑑效組參數。 如果您同時指定鑑效組案例數上限以及鑑效組百分比，在達到案例上限前，會保留案例的百分比。 您指定的鑑效組百分比為整數，後面接著**百分比**關鍵字，並指定最大案例數目為整數，後面接著**案例**關鍵字。 您可以用任何順序結合這些條件，如下列範例所示：  
  
```  
WITH HOLDOUT (20 PERCENT)   
WITH HOLDOUT (2000 CASES)   
WITH HOLDOUT (20 PERCENT OR 2000 CASES)   
WITH HOLDOUT (2000 CASES OR 20 PERCENT)  
```  
  
 鑑效組種子可控制程序的起點，而且此程序會將案例隨機指派給培訓資料集或測試資料集。 您可以藉由設定鑑效組種子，確保資料分割可以重複。 如果您沒有指定鑑效組種子，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會使用採礦結構的名稱來建立種子。 如果您要為結構重新命名，種子值將會變更。 鑑效組種子參數可以搭配一個或兩個其他鑑效組參數使用。  
  
> [!NOTE]  
>  資料分割資訊會使用定型資料快取，因為若要使用鑑效組，您必須確保**CacheMode**採礦結構的屬性設定為**KeepTrainingData**。 在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中，這是新採礦結構的預設值。 變更**CacheMode**屬性**ClearTrainingCases**上現有的採礦結構，其中包含鑑效組資料分割不會影響已處理的任何採礦模型。 不過，如果<xref:Microsoft.AnalysisServices.MiningStructureCacheMode>未設定為**KeepTrainingData**，鑑效組參數會有任何作用。 也就是說，所有來源資料都將用於培訓，而不會提供任何測試集。 資料分割的定義是利用結構快取的；如果您清除培訓案例的快取，也會清除測試資料的快取以及鑑效組集的定義。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用 DMX 建立包含鑑效組的採礦結構。  
  
### <a name="example-1-adding-a-structure-with-no-training-set"></a>範例 1：加入沒有培訓集的結構  
 下列範例建立稱為 `New Mailing` 的新採礦結構，但不建立任何相關聯的採礦模型，也不使用鑑效組。 若要了解如何將採礦模型加入結構，請參閱[ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md)。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)  
```  
  
### <a name="example-2-specifying-holdout-percentage-and-seed"></a>範例 2：指定鑑效組百分比與種子  
 下列子句可以加到資料行定義清單的後面以定義一個資料集，可用於測試與採礦結構相關聯的所有採礦模型。 此陳述式建立的測試集為 25% 的總輸入案例，但沒有案例數的上限。 並使用 5000 當做建立資料分割的種子。 指定種子時，每次當您處理採礦結構時，只要基礎資料沒有變更，就會為測試集選擇相同的案例。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT) REPEATABLE(5000)  
```  
  
### <a name="example-3-specifying-holdout-percentage-and-max-cases"></a>範例 3：指定鑑效組百分比與最大案例數  
 下列子句建立的測試集包含 25% 的總輸入案例或 2000 個案例，以較少者為準。 由於 0 已被指定為種子，採礦結構的名稱會用來建立種子，系統會使用這個種子，開始取樣輸入案例。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT OR 2000 CASES) REPEATABLE(0)  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

