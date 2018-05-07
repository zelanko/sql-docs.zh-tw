---
title: DISCOVER_SCHEMA_ROWSETS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2299df35b0e736a68e9d8416978dac73ca264974
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="discoverschemarowsets-rowset"></a>DISCOVER_SCHEMA_ROWSETS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者所支援之所有列舉值 (Enumeration Value) 以及任何其他的提供者特定列舉值的名稱、限制、描述和其他資訊。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_SCHEMA_ROWSETS**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_SCHEMA_ROWSETS**資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 DISCOVER_SCHEMA_ROWSETS 資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**schemaName**|**DBTYPE_WSTR**||結構描述或要求的名稱。 此要求會傳回中的值*RequestTypes*列舉型別。|  
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
|**schemaName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
