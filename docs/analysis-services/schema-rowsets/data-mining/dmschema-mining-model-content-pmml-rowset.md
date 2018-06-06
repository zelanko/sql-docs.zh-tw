---
title: DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd478b0185feffad77848f5c727c81931d57f9f5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>DMSCHEMA_MINING_MODEL_CONTENT_PMML 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  傳回採礦模型的 XML 結構。 XML 字串的格式是遵循預測模型標記語言 (PMML 2.1) 標準。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_MODEL_CONTENT_PMML**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||以模型是成員的資料庫名稱來擴展之目錄名稱。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||不合格的結構描述名稱。 不支援此資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**MODEL_NAME**|**DBTYPE_WSTR**||模型名稱。 此資料行不能包含**NULL**。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||模型類型。 它是一個提供者特定的字串。 它可以是**NULL**。|  
|**MODEL_GUID**|**DBTYPE_GUID**||識別模型的 GUID。 不使用 Guid 來識別資料表的提供者傳回**NULL**。|  
|**MODEL_PMML**|**DBTYPE_WSTR**||PMML 格式之模型內容的 XML 表示。|  
|**SIZE**|**DBTYPE_UI4**||在 XML 字串中的位元組數目。|  
|**位置**|**DBTYPE_WSTR**||XML 檔案的位置。 它是**NULL**沒有位置是否可用。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DMSCHEMA_MINING_MODEL_CONTENT_PMML**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
