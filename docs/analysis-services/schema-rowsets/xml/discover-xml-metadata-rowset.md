---
title: "DISCOVER_XML_METADATA 資料列集 |Microsoft 文件"
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
- DISCOVER_XML_METADATA
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_XML_METADATA rowset
ms.assetid: 0befd026-db1b-43ac-b0e6-734abb56a4b1
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d0f2a0a63ff4d08a3a273f303a956b49f4932a21
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discoverxmlmetadata-rowset"></a>DISCOVER_XML_METADATA 資料列集
  傳回描述所要求物件的 XML 文件。 傳回的資料列集永遠都是由一個資料列與一個資料行所組成。  
  
 如果您呼叫[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法**DISCOVER_XML_METATDATA**中的列舉值[RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md)項目，**探索**方法會傳回**DISCOVER_XML_METATDATA**資料列集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_XML_METADATA**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**中繼資料**|**DBTYPE_WSTR**||描述限制要求的物件之 XML 文件。|  
  
 這個結構描述資料列集並未排序。  
  
> [!IMPORTANT]  
>  **DISCOVER_XML_METADATA**無法使用 SELECT 命令語法來查詢資料列集。 不過， **DISCOVER_XML_METADATA**資料列集可以使用查詢<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_XML_METADATA**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**DatabaseID**|**DBTYPE_WSTR**|選擇性。|  
|**DimensionID**|**DBTYPE_WSTR**|選擇性。|  
|**CubeID**|**DBTYPE_WSTR**|選擇性。|  
|**MeasureGroupID**|**DBTYPE_WSTR**|選擇性。|  
|**PartitionID**|**DBTYPE_WSTR**|選擇性。|  
|**PerspectiveID**|**DBTYPE_WSTR**|選擇性。|  
|**DimensionPermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**RoleID**|**DBTYPE_WSTR**|選擇性。|  
|**DatabasePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningModelID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningModelPermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**DataSourceID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningStructureID**|**DBTYPE_WSTR**|選擇性。|  
|**AggregationDesignID**|**DBTYPE_WSTR**|選擇性。|  
|**TraceID**|**DBTYPE_WSTR**|選擇性。|  
|**MiningStructurePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**CubePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**AssemblyID**|**DBTYPE_WSTR**|選擇性。|  
|**MdxScriptID**|**DBTYPE_WSTR**|選擇性。|  
|**DataSourceViewID**|**DBTYPE_WSTR**|選擇性。|  
|**DataSourcePermissionID**|**DBTYPE_WSTR**|選擇性。|  
|**ObjectExpansion**|**DBTYPE_WSTR**|選擇性。|  
  
 限制**ObjectExpansion**，適用於每個主要物件的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 用戶端通常會使用限制來描述要傳回 DDL 的 OLAP 物件，並使用**ObjectExpansion**限制傳回 DDL 中定義的擴充程度。 下表會指出是否允許列舉值[Alter 元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令。  
  
|列舉值|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|只會為要求的物件以及所有下階主要物件，遞迴地傳回要求的名稱/識別碼/時間戳記/狀態。|  
|**ObjectProperties**|展開沒有參考所含物件的要求物件 (包括已展開的次要所含物件)。|  
|**ExpandObject**|與相同*ObjectProperties*，但也會傳回名稱、 識別碼和包含的主要物件的時間戳記。|  
|**ExpandFull**|以遞迴方式將要求的物件完全展開至每個所含物件的底端。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

