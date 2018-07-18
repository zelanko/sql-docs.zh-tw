---
title: DISCOVER_XML_METADATA 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 74b0c33570c9a7f6889e9754eeac7426f72c98ac
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034649"
---
# <a name="discoverxmlmetadata-rowset"></a>DISCOVER_XML_METADATA 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
 限制**ObjectExpansion**，適用於每個主要物件的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 用戶端通常會使用限制來描述要傳回 DDL 的 OLAP 物件，並使用**ObjectExpansion**限制傳回 DDL 中定義的擴充程度。 下表會指出是否允許列舉值[Alter 元素&#40;XMLA&#41; ](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令。  
  
|列舉值|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|只會為要求的物件以及所有下階主要物件，遞迴地傳回要求的名稱/識別碼/時間戳記/狀態。|  
|**ObjectProperties**|展開沒有參考所含物件的要求物件 (包括已展開的次要所含物件)。|  
|**ExpandObject**|與相同*ObjectProperties*，但也會傳回名稱、 識別碼和包含的主要物件的時間戳記。|  
|**ExpandFull**|以遞迴方式將要求的物件完全展開至每個所含物件的底端。|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
