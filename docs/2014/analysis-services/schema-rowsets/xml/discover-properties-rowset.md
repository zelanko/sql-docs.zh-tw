---
title: DISCOVER_PROPERTIES 資料列集 |Microsoft Docs
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
- DISCOVER_PROPERTIES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc02dd29ee02ad4d1730a6af72c5df3c3fee1c55
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271834"
---
# <a name="discoverproperties-rowset"></a>DISCOVER_PROPERTIES 資料列集
  針對指定的資料來源，傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者所支援標準和提供者特定屬性的相關資訊及值清單。 未支援的屬性不會列在傳回的結果集中。  
  
 如果您呼叫[Discover](../../xmla/xml-elements-methods-discover.md)方法`DISCOVER_PROPERTIES`中的列舉值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)項目`Discover`方法會傳回`DISCOVER_PROPERTIES`資料列集...  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_PROPERTIES`資料列集包含下列資料行。  
  
|資料行名稱|類型|長度|描述|  
|-----------------|----------|------------|-----------------|  
|`PropertyName`|`DBTYPE_WSTR`||屬性的名稱。|  
|`PropertyDescription`|`DBTYPE_WSTR`||屬性的可當地語系化的文字描述。 可能會傳回 `NULL`。|  
|`PropertyType`|`DBTYPE_WSTR`||屬性的 XML 資料類型。<br /><br /> 可能會傳回 `NULL`。|  
|`PropertyAccessType`|`DBTYPE_WSTR`||屬性的存取權。 值可以是 `Read`、`Write` 或 `ReadWrite`。|  
|`IsRequired`|`DBTYPE_BOOL`||布林值，指出是否需要屬性。<br /><br /> 如果需要屬性則為 True；如果不需要則為 False。<br /><br /> 可能會傳回 `NULL`。|  
|`Value`|`DBTYPE_WSTR`||屬性目前的值。<br /><br /> 可能會傳回 `NULL`。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_PROPERTIES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`PropertyName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  
