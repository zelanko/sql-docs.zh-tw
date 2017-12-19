---
title: "DISCOVER_PARTITION_STAT 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0660deb042e8b3d0c665152779fc6900833b26d9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="discoverpartitionstat-rowset"></a>DISCOVER_PARTITION_STAT 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]傳回特定資料分割中的彙總統計資料。  
  
 **適用於：**表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_PARTITION_STAT**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**資料庫名稱**|**DBTYPE_WSTR**|Required|包含維度的資料庫名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Required|包含資料分割之 Cube 或表格式模型的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Required|維度中量值群組的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|Required|資料分割的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**AGGREGATION_NAME**|**DBTYPE_WSTR**||彙總的名稱。|  
|**AGGREGATION_SIZE**|**DBTYPE_I8**||彙總的大小。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
