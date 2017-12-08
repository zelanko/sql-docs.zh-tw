---
title: "採礦模型的篩選 (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
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
- attributes [data mining]
- filter syntax [data mining]
- models [Analysis Services], filtering
- filters [data mining]
- filtering data [Analysis Services]
ms.assetid: 0f29c19c-4be3-4bc7-ab60-f4130a10d59c
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8bf35c6bd8086ba6fc61dce76853308c9cb34e2d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="filters-for-mining-models-analysis-services---data-mining"></a>採礦模型的篩選 (Analysis Services - 資料採礦)
  以資料為基礎的模型篩選可協助您建立使用採礦結構中之資料子集的採礦模型。 當您設計採礦結構和資料來源時，篩選可提供彈性，因為您可以根據完整的資料來源檢視來建立單一採礦結構。 然後，您可以建立篩選來單獨使用其中一部分資料進行各種模型的定型和測試，而非針對每個資料子集建立不同的結構和相關模型。  
  
 例如，您可以針對 Customers 資料表和相關資料表定義資料來源檢視。 接著，您可以定義包含所需之所有欄位的單一採礦結構。 最後，您可以建立在特定客戶屬性 (例如 Region) 上篩選的模型。 然後，您可以輕鬆地建立該模型的副本，並且單獨將篩選條件變更為根據不同的區域產生新的模型。  
  
 您可以從這項功能中獲益的某些真實生活狀況包括：  
  
-   針對離散值 (例如性別、區域等等) 建立不同的模型。 例如，服飾店可能會使用客戶人口統計來依據性別建立不同的模型，即使銷售資料來自所有客戶的單一資料來源也一樣。  
  
-   建立並測試相同資料的多個群組 (例如 20-30 歲、20-40 歲與 20-25 歲的比較)，藉以嘗試各種模型。  
  
-   針對巢狀資料表內容指定複雜的篩選，例如只有當客戶至少購買兩個特定項目時，才會在模型中加入案例。  
  
 本節將說明如何建立、使用和管理採礦模型的篩選。  
  
## <a name="creating-model-filters"></a>建立模型篩選  
 您可以利用下列方式來建立和套用篩選：  
  
-   使用資料採礦設計師中的 **[採礦模型]** 索引標籤並搭配篩選編輯器對話方塊來建立條件。  
  
-   直接在採礦模型的 **[篩選]** 屬性中輸入篩選運算式。  
  
-   使用分析管理物件 (AMO)，以程式設計方式設定模型的篩選條件。  
  
### <a name="creating-model-filters-using-data-mining-designer"></a>使用資料採礦設計師來建立模型篩選  
 您可以變更採礦模型的 **Filter** 屬性，藉以在資料採礦設計師中篩選模型。 您可以直接在 **[屬性]** 窗格中輸入篩選運算式，也可以開啟篩選對話方塊來建立條件。  
  
 目前提供了兩個篩選對話方塊。 第一個對話方塊可讓您建立套用至案例資料表的條件。 如果資料來源包含多份資料表，您首先要選取一份資料表，然後選取資料行並指定套用至該資料行的運算子與條件。 您可以使用 **AND**/**OR** 運算子。 可用來定義值的運算子會因資料行包含離散值或連續值而不同。 例如，如果包含連續值，您就可以使用 **greater than** 和 **less than** 運算子。 不過，若是離散值，您只能使用 **= (等於)**、 **!= (不等於)**和 **is null** 運算子。  
  
> [!NOTE]  
>  不支援 **LIKE** 關鍵字。 如果您想要加入多個離散屬性，就必須建立不同的條件，然後使用 **OR** 運算子來連結它們。  
  
 如果這些條件很複雜，您可以使用第二個篩選對話方塊來一次使用一份資料表。 當您關閉第二個篩選對話方塊時，運算式會進行評估，然後與案例資料表中已設定於其他資料行的篩選條件結合。  
  
### <a name="creating-filters-on-nested-tables"></a>建立巢狀資料表的篩選  
 如果資料來源檢視包含巢狀資料表，您就可以使用第二個篩選對話方塊，針對巢狀資料表中的資料列建立條件。  
  
 例如，如果您的案例資料表與客戶有關，而且巢狀資料表顯示某位客戶已經購買的產品，您就可以在巢狀資料表篩選中使用下列語法，藉以針對已經購買特定項目的客戶建立篩選： `[ProductName]=’Water Bottle’ OR ProductName=’Water Bottle Cage'`。  
  
 您也可以使用 **EXISTS** 或 **NOT EXISTS** 關鍵字和子查詢，藉以篩選巢狀資料表中是否存在特定值。 這可讓您建立 `EXISTS (SELECT * FROM Products WHERE ProductName=’Water Bottle’)`等條件。 如果巢狀資料表至少有一個資料列包含 `EXISTS SELECT(<subquery>)` 值， **就會傳回** true `Water Bottle`。  
  
 您可以結合案例資料表的條件與巢狀資料表的條件。 例如，下列語法包含案例資料表的條件 (`Age > 30` )、巢狀資料表的子查詢 (`EXISTS (SELECT * FROM Products)`)，以及巢狀資料表的多項條件 (`WHERE ProductName=’Milk’  AND Quantity>2`) )。  
  
```  
(Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName=’Milk’  AND Quantity>2) )  
```  
  
 當您建立篩選完成時，篩選文字就會由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]進行評估、轉譯成 DMX 運算式，然後與模型一起儲存。  
  
 如需如何使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]之篩選對話方塊的指示，請參閱 [Apply a Filter to a Mining Model](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)(將篩選套用至採礦模型)。  
  
## <a name="managing-mining-model-filters"></a>管理採礦模型篩選  
 以資料為基礎的模型篩選會大幅簡化管理採礦結構和採礦模型的工作，因為您可以輕鬆地建立以相同結構為基礎的多個模型。 您也可以快速地建立現有採礦模型的副本，然後單獨變更篩選條件。 但是，篩選可能會產生一些混淆。  
  
 以下是有關如何針對採礦模型管理及解譯篩選的一些常見問題：  
  
### <a name="how-can-i-tell-whether-a-filter-is-being-used"></a>我要如何判斷是否使用篩選？  
 有多種方法可判斷篩選是否套用到模型：  
  
-   在設計師中按一下 **[採礦模型]** 索引標籤，並開啟 **[屬性]**，然後檢視採礦模型的 **Filter** 屬性。  
  
-   DMV、DMSCHEMA_MINING_MODELS 會輸出包含篩選文字的資料行。 您可以針對 DMV 使用以下查詢來傳回模型的名稱以及其篩選：  
  
    ```  
    SELECT MODEL_NAME, [FILTER]   
    FROM $SYSTEM.DMSCHEMA_MINING_MODELS  
  
    ```  
  
-   您可以在 AMO 中取得 MiningModel 物件的 Filter 屬性值，或是檢查 XMLA 中的 Filter 元素。  
  
 您或許也可以為模型建立命名慣例來反映篩選的內容。 這可讓您更方便區分相關的模型。  
  
### <a name="how-can-i-save-a-filter"></a>如何儲存篩選？  
 篩選運算式會儲存成指令碼，並且與相關聯的採礦模型或巢狀資料表一起儲存。 如果您刪除了篩選文字，就只能手動重新建立篩選運算式，才能加以還原。 因此，如果您建立複雜的篩選運算式，就應該建立篩選文字的備份副本。  
  
### <a name="why-cant-i-see-any-effects-from-the-filter"></a>為什麼看不到篩選的任何作用？  
 每當您變更或加入篩選運算式時，就必須重新處理結構和模型，然後才能檢視篩選的效果。  
  
### <a name="why-do-i-see-filtered-attributes-in-prediction-query-results"></a>為什麼在預測查詢結果中看到已篩選的屬性？  
 將篩選套用至模型時，它只會影響用於定型模型的選定案例。 篩選不會影響模型已知的屬性或是變更或隱藏資料來源中的資料。 因此，針對模型所做的查詢可以傳回其他案例類型的預測，而模型所使用之值的下拉式清單可能會顯示篩選所排除的屬性值。  
  
 例如，假設您只使用 20-30 歲婦女的案例來定型 [Bike Buyer] 模型。 您依然可以執行預測查詢來預測男性購買自行車的機率，或是預測 30-40 歲婦女的結果。 這是因為資料來源中的屬性和值會定義理論上可能發生的狀況，而案例則會定義用於定型的發生狀況。 但是，這些查詢將會傳回極小的機率，因為定型資料不包含任何有目標值的案例。  
  
 如果您必須將模型中的屬性值完全隱藏或匿名，有許多選擇可以採用：  
  
-   篩選屬於資料來源檢視定義之一部分或是關聯式資料來源中的內送資料。  
  
-   為屬性值加上遮罩或編碼。  
  
-   將已排除的值摺疊到類別目錄中，當做採礦結構定義的一部分。  
  
## <a name="related-resources"></a>相關資源  
 如需篩選語法的詳細資訊以及篩選運算式的範例，請參閱 [模型篩選語法和範例 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)。  
  
 如需在測試採礦模型時如何使用模型篩選的資訊，請參閱 [Choose an Accuracy Chart Type and Set Chart Options](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)(選擇精確度圖表類型及設定圖表選項)。  
  
## <a name="see-also"></a>請參閱＜  
 [模型篩選語法和範例 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [測試及驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
