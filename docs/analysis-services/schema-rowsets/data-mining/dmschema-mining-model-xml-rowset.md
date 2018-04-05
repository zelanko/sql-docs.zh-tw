---
title: DMSCHEMA_MINING_MODEL_XML 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODEL_XML
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_XML rowset
ms.assetid: f58b00e9-3f72-4cff-b448-21a9fb529772
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b27cfca519f1a5afce1a58bf89a6434f6f85bd34
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingmodelxml-rowset"></a>DMSCHEMA_MINING_MODEL_XML 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]傳回採礦模型的 XML 結構。 XML 字串的格式是遵循預測模型標記語言 (PMML 2.1) 標準。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DMSCHEMA_MINING_MODEL_XML**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||目錄的名稱。 以模型所屬的資料庫名稱來擴展。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||不合格的結構描述名稱。 不支援此資料行[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; 它一律包含**NULL**。|  
|**MODEL_NAME**|**DBTYPE_WSTR**||模型名稱。 此資料行不能包含**NULL**。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||模型類型。 它是一個提供者特定的字串。 它可以是**NULL**。|  
|**MODEL_GUID**|**DBTYPE_GUID**||識別模型的 GUID。 不使用 Guid 來識別資料表的提供者傳回**NULL**。|  
|**MODEL_PMML**|**DBTYPE_WSTR**||PMML 格式之模型內容的 XML 表示。|  
|**大小**|**DBTYPE_UI4**||在 XML 字串中的位元組數目。|  
|**位置**|**DBTYPE_WSTR**||XML 檔案的位置。 它是**NULL**如果實體檔案不會用於儲存體。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 DMSCHEMA_MINING_MODEL_XML 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_W**STR|選擇性。|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>請參閱  
 [資料採礦結構描述資料列集](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
