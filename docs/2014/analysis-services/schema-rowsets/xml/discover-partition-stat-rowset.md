---
title: DISCOVER_PARTITION_STAT 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98db8d43f86cc9acaf612da8180498d22e01d037
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145717"
---
# <a name="discoverpartitionstat-rowset"></a>DISCOVER_PARTITION_STAT 資料列集
  傳回特定資料分割中彙總的相關統計資料。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_PARTITION_STAT`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|必要項|包含維度的資料庫名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|必要項|包含資料分割之 Cube 或表格式模型的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|必要項|維度中量值群組的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|必要項|資料分割的名稱。<br /><br /> 這個資料行是限制清單中的必要項。|  
|`AGGREGATION_NAME`|`DBTYPE_WSTR`||彙總的名稱。|  
|`AGGREGATION_SIZE`|`DBTYPE_I8`||彙總的大小。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  