---
title: "DMSCHEMA_MINING_SERVICES 資料列集 |Microsoft 文件"
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
ms.topic: reference
apiname: DMSCHEMA_MINING_SERVICES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_SERVICES rowset
ms.assetid: 4a672f2f-d637-4def-a572-c18556f83d34
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 87fdcfb688d6e6b7305ef3a46b0de7800e6c4668
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingservices-rowset"></a>DMSCHEMA_MINING_SERVICES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]提供描述每個資料採礦演算法提供者支援。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_SERVICES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|描述|  
|-----------------|--------------------|-----------------|  
|**服務名稱**|**DBTYPE_WSTR**|演算法的名稱。 這個欄位是提供者特定的。|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|此資料行包含描述採礦服務的點陣圖。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]擴展這個資料行具有下列值之一：<br /><br /> **DM_SERVICETYPE_CLASSIFICATION** (**1**)<br /><br /> **DM_SERVICETYPE_CLUSTERING** (**2**)|  
|**SERVICE_DISPLAY_NAME**|**DBTYPE_WSTR**|可當地語系化的演算法顯示名稱。|  
|**SERVICE_GUID**|**DBTYPE_GUID**|演算法的 GUID。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|使用者易記的演算法描述。|  
|**PREDICTION_LIMIT**|**DBTYPE_UI4**|模型與演算法可以提供的最大預測數目。|  
|**SUPPORTED_DISTRIBUTION_FLAGS**|**DBTYPE_WSTR**|以逗號分隔的旗標清單，描述演算法支援的統計散發。 此資料行可包含下列一或多個值：<br /><br /> 「**一般**"<br /><br /> 「**記錄一般**"<br /><br /> 「**統一**"|  
|**SUPPORTED_INPUT_CONTENT_TYPES**|**DBTYPE_WSTR**|以逗號分隔的旗標清單，描述演算法支援的輸入內容類型。 此資料行可包含下列一或多個值：<br /><br /> 「**金鑰**"<br /><br /> 「**離散**"<br /><br /> 「**連續**"<br /><br /> 「**DISCRETIZED**"<br /><br /> 「**ORDERED**"<br /><br /> 「 索引鍵**順序**"<br /><br /> 「**CYCLICAL**"<br /><br /> 「**機率**"<br /><br /> 「**變異數**"<br /><br /> 「**STDEV**"<br /><br /> 「**支援**"<br /><br /> 「**機率變異數**"<br /><br /> 「**機率 STDEV**"<br /><br /> 「**KEY TIME**"|  
|**SUPPORTED_PREDICTION_CONTENT_TYPES**|**DBTYPE_WSTR**|以逗號分隔的旗標清單，描述演算法支援的預測內容類型。 此資料行可包含下列一或多個值：<br /><br /> 「**金鑰**"<br /><br /> 「**離散**"<br /><br /> 「**連續**"<br /><br /> 「**DISCRETIZED**"<br /><br /> 「**ORDERED**"<br /><br /> 「 索引鍵**順序**"<br /><br /> 「**CYCLICAL**"<br /><br /> 「**機率**"<br /><br /> 「**變異數**"<br /><br /> 「**STDEV**"<br /><br /> 「**支援**"<br /><br /> 「**機率變異數**"<br /><br /> 「**機率 STDEV**"<br /><br /> "KEY TIME"|  
|**SUPPORTED_MODELING_FLAGS**|**DBTYPE_WSTR**|以逗號分隔的清單，其中包含演算法支援的模型旗標。 此資料行可包含下列一或多個值：<br /><br /> 「**MODEL_EXISTENCE_ONLY**"<br /><br /> 「**迴歸輸入變數**"<br /><br /> <br /><br /> 請注意，您也可以定義提供者特有的旗標。|  
|**SUPPORTED_SOURCE_QUERY**|**DBTYPE_WSTR**|支援這個資料行的目的，是為了回溯相容性。|  
|**TRAINING_COMPLEXITY**|**DBTYPE_I4**|定型預期花費的時間長度：<br /><br /> **DM_TRAINING_COMPLEXITY_LOW**表示執行時間是相對較短，而且與輸入成比例。<br /><br /> **DM_TRAINING_COMPLEXITY_MEDIUM**表示執行時間可能較長，但通常與輸入成比例。<br /><br /> **DM_TRAINING_COMPLEXITY_HIGH**表示執行時間很長，而且它可能會成長以指數方式關聯性中的定型案例數目。|  
|**PREDICTION_COMPLEXITY**|**DBTYPE_I4**|預期可能需要花費的時間長度：<br /><br /> **DM_PREDICTION_COMPLEXITY_LOW**表示執行時間是相對較短，而且與輸入成比例。<br /><br /> **DM_PREDICTION_COMPLEXITY_MEDIUM**表示執行時間可能較長，但通常與輸入成比例。<br /><br /> **DM_PREDICTION_COMPLEXITY_HIGH**表示執行時間很長，而且它可能會成長以指數方式關聯性中的定型案例數目。|  
|**EXPECTED_QUALITY**|**DBTYPE_I4**|使用此演算法產生的模型預期品質。<br /><br /> **DM_EXPECTED_QUALITY_LOW**<br /><br /> **DM_EXPECTED_QUALITY_MEDIUM**<br /><br /> **DM_EXPECTED_QUALITY_HIGH**|  
|**縮放比例**|**DBTYPE_I4**|演算法的延展性：<br /><br /> **DM_SCALING_LOW**<br /><br /> **DM_SCALING_MEDIUM**<br /><br /> **DM_SCALING_HIGH**|  
|**ALLOW_INCREMENTAL_INSERT**|**DBTYPE_BOOL**|布林值，指出演算法是否支援累加定型，也就是根據新的事實資料更新已探索的模式，而不是完全重新探索模式。|  
|**ALLOW_PMML_INITIALIZATION**|**DBTYPE_BOOL**|布林值，指出是否可以根據 PMML 2.1 字串建立採礦模型。<br /><br /> 如果**TRUE**，則採礦演算法支援 PMML 2.1 內容的初始化。|  
|**控制項**|**DBTYPE_I4**|定型中斷時，服務所提供的支援：<br /><br /> **DM_CONTROL_NONE**表示在開始定型模型之後，無法取消演算法。<br /><br /> **DM_CONTROL_CANCEL**指出之後開始定型模型，但必須重新啟動才能繼續定型，可以取消演算法。<br /><br /> **DM_CONTROL_SUSPENDRESUME**指示演算法可以取消和繼續在任何時間，但定型完成之前，沒有可用的結果。<br /><br /> **DM_CONTROL_SUSPENDWITHRESULT**指示演算法可以取消和繼續在任何時間，而且可以取得任何累加的結果。|  
|**ALLOW_DUPLICATE_KEY**|**DBTYPE_BOOL**|布林值，指出案例是否可包含重複的索引鍵。<br /><br /> 如果**VARIANT_TRUE**，案例允許包含重複的索引鍵。|  
|**VIEWER_TYPE**|**DBTYPE_WSTR**|此模型建議使用的檢視器。|  
|**HELP_FILE**|**DBTYPE_WSTR**|(選擇性) 檔案的名稱，這個檔案包含此服務的文件集。|  
|**HELP_CONTEXT**|**DBTYPE_I4**|(選擇性) 此服務的說明內容識別碼。|  
|**MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL**|**DBTYPE_WSTR**|支援的 DDL 版本。 0 表示沒有 DDL 支援。|  
|**MSOLAP_SUPPORTS_OLAP_MINING_MODELS**|**DBTYPE_BOOL**|布林值，指出是否可以建立 OLAP 採礦模型。<br /><br /> 如果**TRUE**，可以建立 OLAP 採礦模型。 需要**MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL**為非零。|  
|**MSOLAP_SUPPORTS_DATA_MINING_DIMENSIONS**|**DBTYPE_BOOL**|布林值，指出是否可以建立資料採礦維度。<br /><br /> 如果**TRUE**，可以建立資料採礦維度。|  
|**MSOLAP_SUPPORTS_DRILLTHROUGH**|**DBTYPE_BOOL**|布林值，指出服務是否支援鑽研功能。<br /><br /> 如果**TRUE**，服務支援鑽研功能。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_SERVICES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**服務名稱**|**DBTYPE_WSTR**|選擇性。|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|選擇性。|  
  
## <a name="see-also"></a>請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
