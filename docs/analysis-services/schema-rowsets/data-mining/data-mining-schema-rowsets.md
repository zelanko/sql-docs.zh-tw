---
title: 資料採礦結構描述資料列 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0324ee3b35f4b45162b9646d2d0e9cfeada47551
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="data-mining-schema-rowsets"></a>資料採礦結構描述資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  正在執行的伺服器[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]支援下列資料採礦結構描述資料列集。 若要檢查特定 XML/A 提供者是否支援特定的資料列集，請使用[DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)含有資料列集[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
 在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中，資料採礦結構描述資料列集會以 Transact-SQL 語言中的資料表格式，在 $SYSTEM 結構描述中公開。 例如，在 Analysis Services 執行個體上的下列查詢會傳回在目前執行個體上可用的結構描述清單。  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>本節內容  
  
|結構描述資料列集|Description|  
|-------------------|-----------------|  
|[DMSCHEMA_MINING_COLUMNS 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|描述部署在伺服器上所有定義之資料採礦模型的個別資料行。|  
|[DMSCHEMA_MINING_FUNCTIONS 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|描述可與安裝在伺服器上的每個資料採礦演算法，搭配使用的預測函數與採礦函數。|  
|[DMSCHEMA_MINING_MODEL_CONTENT 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|允許用戶端應用程式瀏覽定型資料採礦模型的內容。|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|傳回採礦模型內容的 XML (PMML 2.1) 表示。|  
|[DMSCHEMA_MINING_MODEL_XML 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|傳回採礦模型的 XML (PMML 2.1) 結構。 這是與 DMSCHEMA_MINING_MODEL_PMML 相同的結構描述，是為了回溯相容性而保留的。|  
|[DMSCHEMA_MINING_MODELS 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|列舉在伺服器上部署的資料採礦模型。|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|提供參數清單，這些參數可用以設定每個安裝在伺服器上的資料採礦演算法之行為。|  
|[DMSCHEMA_MINING_SERVICES 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|提供伺服器上可用之每個資料採礦演算法的描述。|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|描述在伺服器上部署之所有採礦結構的個別資料行。|  
|[DMSCHEMA_MINING_STRUCTURES 資料列集](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|列舉採礦結構的資訊。|  
  
 此處所列的所有結構描述資料列所執行的伺服器支援[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 結構描述資料列集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [資料採礦結構描述資料列集&#40;SSAs&#41;](../../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
