---
title: DMSCHEMA_MINING_MODELS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 708a1b58f99e7257369351d82d54f45a863c0ca1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingmodels-rowset"></a>DMSCHEMA_MINING_MODELS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  列舉目前目錄中的資料採礦模型。 **DMSCHEMA_MINING_MODELS**資料列集包含模型名稱、 處理日期，以及與每個採礦模型相關聯的採礦演算法等資訊。  
  
 。 **DMSCHEMA_MINING_MODELS**結構描述資料列集是非常類似於[DBSCHEMA_TABLES](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md)結構描述資料列集，可以使用相同的方式。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_MODELS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|目錄的名稱。 以模型所屬的資料庫名稱來擴展。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|不合格的結構描述名稱。 不支援此資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|採礦模型名稱。 此資料行包含採礦模型的名稱，而且永遠都不會是空的。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|模型類型。|  
|**MODEL_GUID**|**DBTYPE_GUID**|模型的 GUID。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|模型的使用者易記描述。|  
|**MODEL_PROPID**|**DBTYPE_UI4**|模型的屬性識別碼。 不支援此資料行[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**|建立模型的日期。|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**|上次修改模型定義的日期。|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|識別該模型所使用之資料採礦演算法類型的列舉。 這個類型可以是下列其中一個值：<br /><br /> **DM_SERVICETYPE_CLASSIFICATION** (1)<br /><br /> **DM_SERVICETYPE_SEGMENTATION**(2)<br /><br /> **DM_SERVICETYPE_ 關聯**(4)<br /><br /> **DM_SERVICETYPE_ DENSITY_ESTIMATE**(8)<br /><br /> **DM_SERVICETYPE_SEQUENCE**(16)|  
|**服務名稱**|**DBTYPE_WSTR**|該模型所使用之資料採礦演算法的提供者特定名稱。|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**|用以建立採礦模型的陳述式。|  
|**PREDICTION_ENTITY**|**DBTYPE_WSTR**|以逗號分隔的清單，指出可以預測哪些採礦資料行。|  
|**IS_POPULATED**|**DBTYPE_BOOL**|指出模型是否已擴展的布林旗標。<br /><br /> **TRUE**如果模型是已填入，否則**FALSE**。|  
|**MINING_PARAMETERS**|**DBTYPE_WSTR**|建立此模型時所使用的參數以逗號分隔的清單。|  
|**MINING_STRUCTURE**|**DBTYPE_WSTR**|模型所依據之採礦結構的識別碼。|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**|模型上次處理的日期。|  
|**MSOLAP_IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|指出模型是否支援鑽研的布林旗標。|  
|**篩選器**|**DBTYPE_WSTR**|與採礦模型關聯的篩選運算式。<br /><br /> NULL 或是空的字串表示未套用任何篩選。|  
|**TRAINING_SET_SIZE**|**DBTYPE_UIS**|在處理過結構之後且模型已套用任何篩選之後，採礦模型定型集內所包含的案例數目。|  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_MODELS**上表中的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|選擇性。|  
|**服務名稱**|**DBTYPE_WSTR**|選擇性。|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|選擇性。|  
|**MINING_STRUCTURE**|**DBTYPE_WSTR**|選擇性。|  
  
 如需如何查詢此資料列集的範例，請參閱[查詢參數用來建立採礦模型](../../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
