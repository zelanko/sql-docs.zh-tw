---
title: DISCOVER_ENUMERATORS 資料列集 |Microsoft 文件
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
- DISCOVER_ENUMERATORS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2c4eb36f93faba7f32352de41d5c6fde4e0dac2c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136726"
---
# <a name="discoverenumerators-rowset"></a>DISCOVER_ENUMERATORS 資料列集
  針對特定的資料來源，傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 所支援之列舉值 (Enumerator) 的名稱、資料類型和列舉 (Enumeration) 值的清單。 XMLA 提供者會發行它能辨識的所有列舉常數。  
  
 如果您呼叫[探索](../../xmla/xml-elements-methods-discover.md)方法`DISCOVER_ENUMERATORS`中的列舉值[RequestType](../../xmla/xml-elements-properties/type-element-xmla.md)項目，`Discover`方法會傳回`DISCOVER_ENUMERATORS`結構描述資料列。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 每個列舉值都有多個元素，列舉中的每個值都有一個。 代表每個列舉值的資料列集是扁平的，而且屬於同一列舉的元素可以使用重複的列舉值名稱。  
  
 `DISCOVER_ENUMERATORS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`EnumName`|`DBTYPE_WSTR`||包含一組值的列舉值名稱。|  
|`EnumDescription`|`DBTYPE_WSTR`||列舉值的可當地語系化描述。 可以是`NULL`。|  
|`EnumType`|`DBTYPE_WSTR`||列舉 (Enumeration) 值的資料類型。|  
|`ElementName`|`DBTYPE_WSTR`||列舉值集合內其中一個值元素的名稱。<br /><br /> 範例：`TDP`|  
|`ElementDescription`|`DBTYPE_WSTR`||(選擇性) 元素的可當地語系化描述。 可以是`NULL`。|  
|`ElementValue`|`DBTYPE_WSTR`||元素的值。 可以是`NULL`。<br /><br /> 範例：`01`|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DISCOVER_ENUMERATORS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`EnumName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  