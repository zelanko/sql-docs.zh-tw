---
title: DMSCHEMA_MINING_SERVICES 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_SERVICES
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICES rowset
ms.assetid: 4a672f2f-d637-4def-a572-c18556f83d34
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e6ccfdba24d7bc23b97eb15e61321f82e5ab1d9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278216"
---
# <a name="dmschemaminingservices-rowset"></a>DMSCHEMA_MINING_SERVICES 資料列集
  提供由提供者支援之每個資料採礦演算法的描述。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DMSCHEMA_MINING_SERVICES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||演算法的名稱。 這個欄位是提供者特定的。|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`||此資料行包含描述採礦服務的點陣圖。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 填入此資料行具有下列值之一：<br /><br /> -   `DM_SERVICETYPE_CLASSIFICATION` (`1`)<br />-   `DM_SERVICETYPE_CLUSTERING` (`2`)|  
|`SERVICE_DISPLAY_NAME`|`DBTYPE_WSTR`||可當地語系化的演算法顯示名稱。|  
|`SERVICE_GUID`|`DBTYPE_GUID`||演算法的 GUID。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||使用者易記的演算法描述。|  
|`PREDICTION_LIMIT`|`DBTYPE_UI4`||模型與演算法可以提供的最大預測數目。|  
|`SUPPORTED_DISTRIBUTION_FLAGS`|`DBTYPE_WSTR`||以逗號分隔的旗標清單，描述演算法支援的統計散發。 此資料行可包含下列一或多個值：<br /><br /> -   "`NORMAL`"<br />-   "`LOG NORMAL`"<br />-   "`UNIFORM`"|  
|`SUPPORTED_INPUT_CONTENT_TYPES`|`DBTYPE_WSTR`||以逗號分隔的旗標清單，描述演算法支援的輸入內容類型。 此資料行可包含下列一或多個值：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-「 金鑰`SEQUENCE`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-   "`KEY TIME`"|  
|`SUPPORTED_PREDICTION_CONTENT_TYPES`|`DBTYPE_WSTR`||以逗號分隔的旗標清單，描述演算法支援的預測內容類型。 此資料行可包含下列一或多個值：<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-「 金鑰`SEQUENCE`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-「 索引鍵時間 」|  
|`SUPPORTED_MODELING_FLAGS`|`DBTYPE_WSTR`||以逗號分隔的清單，其中包含演算法支援的模型旗標。 此資料行可包含下列一或多個值：<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> 也可以定義提供者特定的旗標。|  
|`SUPPORTED_SOURCE_QUERY`|`DBTYPE_WSTR`||-此資料行被支援回溯相容性。|  
|`TRAINING_COMPLEXITY`|`DBTYPE_I4`||定型預期花費的時間長度：<br /><br /> -   `DM_TRAINING_COMPLEXITY_LOW` 表示執行時間會相對較短，而且它是與輸入成比例。<br />-   **DM_TRAINING_COMPLEXITY_MEDIUM**指出執行的時間可能會很長，但通常與輸入成比例。<br />-   **DM_TRAINING_COMPLEXITY_HIGH**表示執行時間很長，而且它可能會以指數方式成長關聯性中的定型案例數目。|  
|`PREDICTION_COMPLEXITY`|`DBTYPE_I4`||預期可能需要花費的時間長度：<br /><br /> -   **DM_PREDICTION_COMPLEXITY_LOW**表示執行時間會相對較短，而且與輸入成比例。<br />-   **DM_PREDICTION_COMPLEXITY_MEDIUM**指出執行的時間可能會很長，但通常與輸入成比例。<br />-   **DM_PREDICTION_COMPLEXITY_HIGH**表示執行時間很長，而且它可能會以指數方式成長關聯性中的定型案例數目。|  
|`EXPECTED_QUALITY`|`DBTYPE_I4`||使用此演算法產生的模型預期品質。<br /><br /> -   `DM_EXPECTED_QUALITY_LOW`<br />-   `DM_EXPECTED_QUALITY_MEDIUM`<br />-   **DM_EXPECTED_QUALITY_HIGH**|  
|`SCALING`|`DBTYPE_I4`||演算法的延展性：<br /><br /> -   **DM_SCALING_LOW**<br />-   `DM_SCALING_MEDIUM`<br />-   **DM_SCALING_HIGH**|  
|`ALLOW_INCREMENTAL_INSERT`|`DBTYPE_BOOL`||布林值，指出演算法是否支援累加定型，也就是根據新的事實資料更新已探索的模式，而不是完全重新探索模式。|  
|`ALLOW_PMML_INITIALIZATION`|`DBTYPE_BOOL`||布林值，指出是否可以根據 PMML 2.1 字串建立採礦模型。<br /><br /> 如果是 `TRUE`，則採礦演算法支援 PMML 2.1 內容的初始化。|  
|`CONTROL`|`DBTYPE_I4`||定型中斷時，服務所提供的支援：<br /><br /> -   `DM_CONTROL_NONE` 表示在啟動來定型模型之後，無法取消演算法。<br />-   `DM_CONTROL_CANCEL` 指出之後開始定型模型，但必須先將它重新啟動，才能繼續定型，可以取消演算法。<br />-   `DM_CONTROL_SUSPENDRESUME` 表示演算法可以取消和繼續在任何時間，但定型完成之前，未提供結果。<br />-   `DM_CONTROL_SUSPENDWITHRESULT` 表示演算法可以取消和繼續在任何時間，而且可以取得任何累加的結果。|  
|`ALLOW_DUPLICATE_KEY`|`DBTYPE_BOOL`||布林值，指出案例是否可包含重複的索引鍵。<br /><br /> 如果為 `VARIANT_TRUE`，則案例允許包含重複的索引鍵。|  
|`VIEWER_TYPE`|`DBTYPE_WSTR`||此模型建議使用的檢視器。|  
|`HELP_FILE`|`DBTYPE_WSTR`||(選擇性) 檔案的名稱，這個檔案包含此服務的文件集。|  
|`HELP_CONTEXT`|`DBTYPE_I4`||(選擇性) 此服務的說明內容識別碼。|  
|`MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL`|`DBTYPE_WSTR`||支援的 DDL 版本。 0 表示沒有 DDL 支援。|  
|`MSOLAP_SUPPORTS_OLAP_MINING_MODELS`|`DBTYPE_BOOL`||布林值，指出是否可以建立 OLAP 採礦模型。<br /><br /> 如果為 `TRUE` 則可以建立 OLAP 採礦模型。 需要 `MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL` 為非零值。|  
|`MSOLAP_SUPPORTS_DATA_MINING_DIMENSIONS`|`DBTYPE_BOOL`||布林值，指出是否可以建立資料採礦維度。<br /><br /> 如果為 `TRUE`，則可以建立資料採礦維度。|  
|`MSOLAP_SUPPORTS_DRILLTHROUGH`|`DBTYPE_BOOL`||布林值，指出服務是否支援鑽研功能。<br /><br /> 如果為 `TRUE`，則服務支援鑽研功能。|  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DMSCHEMA_MINING_SERVICES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
