---
title: DISCOVER_PROPERTIES 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DISCOVER_PROPERTIES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_PROPERTIES rowset
ms.assetid: 3e2b50e2-3855-4091-8b02-4968e8e57d4c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f37cf116c4d31dbd63ba13b575a91fa042350863
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="discoverproperties-rowset"></a>DISCOVER_PROPERTIES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  針對指定的資料來源，傳回 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) 提供者所支援標準和提供者特定屬性的相關資訊及值清單。 未支援的屬性不會列在傳回的結果集中。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_PROPERTIES**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_PROPERTIES**資料列集...  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_PROPERTIES**資料列集包含下列資料行。  
  
|資料行名稱|型別|長度|Description|  
|-----------------|----------|------------|-----------------|  
|**屬性名稱**|**DBTYPE_WSTR**||屬性的名稱。|  
|**Propid**|**DBTYPE_WSTR**||屬性的可當地語系化的文字描述。 可能會傳回**NULL**。|  
|**PropertyType**|**DBTYPE_WSTR**||屬性的 XML 資料類型。<br /><br /> 可能會傳回**NULL**。|  
|**PropertyAccessType**|**DBTYPE_WSTR**||屬性的存取權。 這個值可以是**讀取**，**寫入**，或**ReadWrite**。|  
|**IsRequired**|**DBTYPE_BOOL**||布林值，指出是否需要屬性。<br /><br /> 如果需要屬性則為 True；如果不需要則為 False。<br /><br /> 可能會傳回**NULL**。|  
|**值**|**DBTYPE_WSTR**||屬性目前的值。<br /><br /> 可能會傳回**NULL**。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_PROPERTIES**上下表所列的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**屬性名稱**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
