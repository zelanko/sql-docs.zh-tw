---
title: "DISCOVER_ENUMERATORS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_ENUMERATORS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 66ad0a7e82cb1b74108a1275a9e0a7363183d051
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discoverenumerators-rowset"></a>DISCOVER_ENUMERATORS 資料列集
  針對特定的資料來源，傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 所支援之列舉值 (Enumerator) 的名稱、資料類型和列舉 (Enumeration) 值的清單。 XMLA 提供者會發行它能辨識的所有列舉常數。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_ENUMERATORS**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_ENUMERATORS**結構描述資料列。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 每個列舉值都有多個元素，列舉中的每個值都有一個。 代表每個列舉值的資料列集是扁平的，而且屬於同一列舉的元素可以使用重複的列舉值名稱。  
  
 **DISCOVER_ENUMERATORS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**列舉名稱**|**DBTYPE_WSTR**||包含一組值的列舉值名稱。|  
|**EnumDescription**|**DBTYPE_WSTR**||列舉值的可當地語系化描述。 可以是**NULL**。|  
|**EnumType**|**DBTYPE_WSTR**||列舉 (Enumeration) 值的資料類型。|  
|**ElementName**|**DBTYPE_WSTR**||列舉值集合內其中一個值元素的名稱。<br /><br /> 範例： **tdp，才能在**|  
|**ElementDescription**|**DBTYPE_WSTR**||(選擇性) 元素的可當地語系化描述。 可以是**NULL**。|  
|**ElementValue**|**DBTYPE_WSTR**||元素的值。 可以是**NULL**。<br /><br /> 範例： **01**|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_ENUMERATORS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**列舉名稱**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

