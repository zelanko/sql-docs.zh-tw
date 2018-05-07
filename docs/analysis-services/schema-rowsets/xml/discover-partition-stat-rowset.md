---
title: DISCOVER_PARTITION_STAT 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a00b6ce9f05b0e22da8ab096d54744602ea2c1b8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="discoverpartitionstat-rowset"></a>DISCOVER_PARTITION_STAT 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  傳回特定資料分割中彙總的相關統計資料。  
  
 **適用於：**表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_PARTITION_STAT**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|必要項|包含維度的資料庫名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|必要項|包含資料分割之 Cube 或表格式模型的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|必要項|維度中量值群組的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|必要項|資料分割的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
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
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
