---
description: 了解 DMX Select 陳述式
title: 瞭解 DMX Select 語句 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 93744da59ad7149203da8fd14179045b63dc798f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395214"
---
# <a name="understanding-the-dmx-select-statement"></a>了解 DMX Select 陳述式
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [SELECT](../dmx/select-dmx.md)語句是您使用資料採礦延伸模組建立的大多數查詢的基礎， (DMX) 的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。 它可以執行許多不同種類的工作，例如瀏覽及針對資料採礦模型預測。  
  
 以下是您可以使用 **SELECT** 語句來完成的工作：  
  
-   瀏覽資料採礦模型。 結構描述資料列集會定義模型的結構。  
  
-   探索採礦模型資料行的可能值。  
  
-   瀏覽指派給採礦模型中之節點的案例，或者取得代表性案例。  
  
-   使用各種輸入來建立預測。  
  
-   複製採礦模型。  
  
 這些工作中的每個都會使用一組不同的資料，我們將會呼叫 *資料網域*。 您可以在語句的 **FROM** 子句中定義資料網域。  
  
-   您想要尋找資料採礦模型本身中的物件，例如定義資料集的規則，或用來進行預測的公式。  
  
     在此情況下，您需要查看儲存在模型本身的中繼資料。 因此，您的資料網域會是資料採礦結構描述資料列集中的資料行。  
  
-   您要從用來建立模型的案例中取得詳細資訊。  
  
     在此情況下，您需要鑽研採礦結構 (也就是您的資料網域)，並查看 [Gender]、[Bike Buyer] 等資料行中的個別資料列。  
  
 **重要事項：** 運算式清單或 **WHERE** 子句中包含的任何事項，都必須來自 **from** 子句所定義的資料網域。 您不能混用資料網域。  
  
##  <a name="select-types"></a><a name="Select_Types"></a> 選取類型  
 **SELECT**語句的語法支援許多不同的工作。 請使用下列模式執行這些工作：  
  
-   [預測](#Predicting)  
  
-   [瀏覽](#Browsing)  
  
-   [複製](#Copying)  
  
-   [鑽研](#Drillthrough)  
  
###  <a name="predicting"></a><a name="Predicting"></a> 預測  
 您可以使用下列查詢類型，根據採礦模型執行預測。  
  
 您可以在預測聯結**SELECT**語句的**FROM**和**WHERE**子句內，包含任何一種流覽或預測**select**語句。  
  
|查詢類型|描述|  
|----------------|-----------------|  
|SELECT FROM [天然] 預測聯結|傳回將採礦模型中的資料行聯結至內部資料來源的資料行所建立的預測。<br /><br /> 這種查詢類型的網域是模型中的可預測資料行，以及輸入資料來源中的資料行。<br /><br /> [從 &#60;模型選取&#62; 預測聯結 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [預測查詢 &#40;資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|選取來源 *\<model>*|只根據採礦模型傳回可預測資料行的最可能狀態。 這種查詢類型是建立具有空白預測聯結之預測的捷徑。<br /><br /> 這種查詢類型的網域是模型中的可預測資料行。<br /><br /> [從 &#60;模型&#62; &#40;DMX&#41;中選取 ](../dmx/select-from-model-dmx.md)<br /><br /> [預測查詢 &#40;資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [回到選取類型](#Select_Types)  
  
###  <a name="browsing"></a><a name="Browsing"></a> 流覽  
 您可以使用下列查詢類型瀏覽採礦模型的內容。  
  
|查詢類型|描述|  
|----------------|-----------------|  
|選取相異來源 *\<model>*|傳回指定資料行之採礦模型的所有狀態值。<br /><br /> 這個查詢類型的資料網域是資料採礦模型。<br /><br /> [選取 [不同于 &#60;模型 &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [內容查詢 &#40;資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|選取 [來源] *\<model>* 。內容|傳回描述採礦模型的內容。<br /><br /> 這個查詢類型的資料網域是內容結構描述資料列集。<br /><br /> [從 &#60;模型&#62; 選取。DMX&#41;內容 &#40;](../dmx/select-from-model-content-dmx.md)<br /><br /> [內容查詢 &#40;資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|選取 [來源] *\<model>* 。DIMENSION_CONTENT|傳回描述採礦模型的內容。<br /><br /> 這個查詢類型的資料網域是內容結構描述資料列集。<br /><br /> [從 &#60;模型&#62; 選取。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|選取 [來源] *\<model>* 。Pmml|針對支援此功能的演算法，傳回採礦模型的預測模型標記語言 (PMML) 表示。<br /><br /> 這種查詢類型的網域是 PMML 結構描述資料列集。<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126283(v=sql.110))|  
  
 [回到選取類型](#Select_Types)  
  
###  <a name="copying"></a><a name="Copying"></a> 複製  
 您可以將採礦模型與其相關聯的採礦結構複製到新模型，然後重新命名陳述式中的模型。  
  
|查詢類型|描述|  
|----------------|-----------------|  
|SELECT INTO *\<new model>*|建立採礦模型的副本。<br /><br /> 這個查詢類型的網域是資料採礦模型。<br /><br /> [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [回到選取類型](#Select_Types)  
  
###  <a name="drillthrough"></a><a name="Drillthrough"></a> 鑽 取  
 您可以使用下列查詢類型，瀏覽用於培訓模型的案例或案例的表示。  
  
|查詢類型|描述|  
|----------------|-----------------|  
|選取 [來源] *\<model>* 。例|傳回用來定型採礦模型的案例。<br /><br /> 這個查詢類型的網域是資料採礦模型。<br /><br /> [從 &#60;模型&#62; 選取。DMX&#41;&#40;案例 ](../dmx/select-from-model-cases-dmx.md)<br /><br /> [使用 DMX 建立鑽研查詢](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|選取 [來源] *\<model>* 。SAMPLE_CASES|傳回範例案例，這是用來定型採礦模型之案例的代表性案例。<br /><br /> 這個查詢類型的網域是資料採礦模型。<br /><br /> [從 &#60;模型&#62; 選取。SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|選取 [來源] *\<structure>* 。 例|從基礎採礦結構傳回詳細的資料列，即使部分詳細資料未用於定型採礦模型亦然。<br /><br /> [從 &#60;結構&#62; 選取。例](../dmx/select-from-structure-cases.md)<br /><br /> [鑽研查詢 &#40;資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [回到選取類型](#Select_Types)  
  
## <a name="see-also"></a>另請參閱  
 [&#40;DMX&#41; 參考的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
