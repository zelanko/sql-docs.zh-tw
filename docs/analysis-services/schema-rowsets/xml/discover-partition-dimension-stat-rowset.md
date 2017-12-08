---
title: "DISCOVER_PARTITION_DIMENSION_STAT 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: bf4626b3-4d6b-4795-bb01-df335fb9c09a
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: eb81657e74e36f6a854b1bca22a1e61b44cde693
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="discoverpartitiondimensionstat-rowset"></a>DISCOVER_PARTITION_DIMENSION_STAT 資料列集
  傳回與資料分割相關聯之維度的統計資料。  
  
 **適用於：**表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_PARTITION_DIMENSION_STAT**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**資料庫名稱**|**DBTYPE_WSTR**|Required|資料庫的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Required|Cube 或表格式模型的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Required|量值群組的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|Required|資料分割的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||維度的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||維度中屬性的名稱。|  
|**ATTRIBUTE_INDEXED**|**DBTYPE_BOOL**||如果為 true，就表示屬性已建立索引，否則為 false。|  
|**ATTRIBUTE_COUNT_MIN**|**DBTYPE_I8**||最小屬性計數。|  
|**ATTRIBUTE_COUNT_MAX**|**DBTYPE_I8**||最大屬性計數。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>請參閱＜  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
