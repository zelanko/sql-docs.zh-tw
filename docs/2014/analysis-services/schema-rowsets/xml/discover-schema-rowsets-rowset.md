---
title: DISCOVER_SCHEMA_ROWSETS 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DISCOVER_SCHEMA_ROWSETS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_SCHEMA_ROWSETS rowset
ms.assetid: e5012aa0-6ef8-497f-96c1-2772e2394f62
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e8071da248e9c7d69a76a22f7c339fad0a217295
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024069"
---
# <a name="discoverschemarowsets-rowset"></a>DISCOVER_SCHEMA_ROWSETS 資料列集
  傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者所支援之所有列舉值 (Enumeration Value) 以及任何其他的提供者特定列舉值的名稱、限制、描述和其他資訊。  
  
 如果您呼叫[探索](../../xmla/xml-elements-methods-discover.md)方法`DISCOVER_SCHEMA_ROWSETS`中的列舉值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)項目，`Discover`方法會傳回`DISCOVER_SCHEMA_ROWSETS`資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 DISCOVER_SCHEMA_ROWSETS 資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`SchemaName`|`DBTYPE_WSTR`||結構描述或要求的名稱。 此要求會傳回中的值*RequestTypes*列舉型別。|  
|`SchemaGuid`|`DBTYPE_GUID`||結構描述的 GUID。|  
|`Restrictions`|`DBTYPE_HCHAPTER`||提供者所支援的限制陣列。|  
|`Description`|`DBTYPE_WSTR`||結構描述的可當地語系化描述。|  
|`RestrictionsMask`|`DBTYPE_UI8`|||  
  
 這個結構描述資料列集並未排序。  
  
 如果提供者支援 DBSCHEMA_MEMBERS 結構描述資料列集的三項限制，則 `Restrictions` 陣列可能會傳回下列結果。 結果中的元素是指結構描述中的資料行名稱。  
  
```  
<Restrictions>  
      <CATALOG_NAME type="string" />   
      <SCHEMA_NAME type="string" />   
      <CUBE_NAME type="string" />   
</Restrictions>  
```  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_SCHEMA_ROWSETS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`SchemaName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  