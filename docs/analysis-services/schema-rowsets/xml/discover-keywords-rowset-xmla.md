---
title: "DISCOVER_KEYWORDS 資料列集 (XMLA) |Microsoft 文件"
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
- DISCOVER_KEYWORDS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 99945e53-3a1b-4d7b-9aff-712977db8b2d
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 232bbcfb4d5cf1dfc181a0c6d8879e4390f61a9e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discoverkeywords-rowset-xmla"></a>DISCOVER_KEYWORDS 資料列集 (XMLA)
  傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者所保留關鍵字的相關資訊。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_KEYWORDS**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_KEYWORDS**資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_KEYWORDS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**關鍵字**|**DBTYPE_WSTR**||提供者保留的所有關鍵字的清單。<br /><br /> 範例： **AND**|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_KEYWORDS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**關鍵字**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)   
 [DISCOVER_LITERALS 資料列集](../../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)  
  
  

