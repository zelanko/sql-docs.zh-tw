---
title: "DISCOVER_SCHEMA_ROWSETS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_SCHEMA_ROWSETS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_SCHEMA_ROWSETS rowset
ms.assetid: e5012aa0-6ef8-497f-96c1-2772e2394f62
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4e5a3923ff0137e81064224fb6a2dfd9ca98f435
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="discoverschemarowsets-rowset"></a>DISCOVER_SCHEMA_ROWSETS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]傳回名稱、 限制、 描述和所有列舉值和所支援的任何其他的提供者特定列舉值的其他資訊[!INCLUDE[msCoName](../../../includes/msconame-md.md)]XML for Analysis (XMLA) 提供者。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_SCHEMA_ROWSETS**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_SCHEMA_ROWSETS**資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 DISCOVER_SCHEMA_ROWSETS 資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SchemaName**|**DBTYPE_WSTR**||結構描述或要求的名稱。 此要求會傳回中的值*RequestTypes*列舉型別。|  
|**SchemaGuid**|**DBTYPE_GUID**||結構描述的 GUID。|  
|**限制**|**DBTYPE_HCHAPTER**||提供者所支援的限制陣列。|  
|**說明**|**DBTYPE_WSTR**||結構描述的可當地語系化描述。|  
|**RestrictionsMask**|**DBTYPE_UI8**|||  
  
 這個結構描述資料列集並未排序。  
  
 提供者支援 DBSCHEMA_MEMBERS 結構描述資料列集，三個限制**限制**陣列可能會傳回下列結果。 結果中的元素是指結構描述中的資料行名稱。  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_SCHEMA_ROWSETS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**SchemaName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
