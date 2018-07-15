---
title: DISCOVER_PARTITION_DIMENSION_STAT 資料列集 |Microsoft Docs
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
ms.assetid: bf4626b3-4d6b-4795-bb01-df335fb9c09a
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f4dc209f985cafe804f81fa54fa68c56655d3e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310738"
---
# <a name="discoverpartitiondimensionstat-rowset"></a>DISCOVER_PARTITION_DIMENSION_STAT 資料列集
  傳回與資料分割相關聯之維度的統計資料。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_PARTITION_DIMENSION_STAT`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|必要項|資料庫的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|必要項|Cube 或表格式模型的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|必要項|量值群組的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|必要項|資料分割的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||維度的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||維度中屬性的名稱。|  
|`ATTRIBUTE_INDEXED`|`DBTYPE_BOOL`||如果為 true，就表示屬性已建立索引，否則為 false。|  
|`ATTRIBUTE_COUNT_MIN`|`DBTYPE_I8`||最小屬性計數。|  
|`ATTRIBUTE_COUNT_MAX`|`DBTYPE_I8`||最大屬性計數。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  
