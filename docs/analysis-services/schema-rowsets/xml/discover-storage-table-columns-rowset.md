---
title: "DISCOVER_STORAGE_TABLE_COLUMNS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6390df460f9a1ec495f7201d2d715d85d3999846
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discoverstoragetablecolumns-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMNS 資料列集
  提供在資料行層級中，有關 SharePoint 或表格式模式下執行 Analysis Services 資料庫所用儲存體資料表的資訊。  
  
 **適用於：** 表格式模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_STORAGE_TABLE_COLUMNS**資料列集包含下列資料行。  
  
|**資料行名稱**|**類型指標**|**限制**|**說明**|  
|---------------------|------------------------|---------------------|---------------------|  
|**資料庫名稱**|**DBTYPE_WSTR**|是|指定包含資料表的資料庫名稱。 如果省略，就會使用目前的資料庫。<br /><br /> **DISCOVER_STORAGE_TABLE_COLUMNS**資料列集可能會限制使用此資料行。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|是|指定包含資料表的 Cube 或模型。<br /><br /> **DISCOVER_STORAGE_TABLES**資料列集可能會限制使用此資料行。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|是|量值群組的名稱。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||維度的名稱。|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||屬性的名稱。|  
|**TABLE_ID**|**DBTYPE_WSTR**||資料表的識別碼。|  
|**COLUMN_ID**|**DBTYPE_ WSTR**||資料行的識別碼。 資料行識別碼是 xVelocity 記憶體中分析引擎 (VertiPaq) 內部的識別碼，因此，僅提供資訊之用。|  
|**COLUMN_TYPE**|**DBTYPE_WSTR**||資料行的類型。 資料行類型是 xVelocity 記憶體中分析引擎 (VertiPaq) 內部的類型，因此，僅提供資訊之用。<br /><br /> BASIC_DATA<br /><br /> HIERARCHY_DATAID_TO_POSITION<br /><br /> HIERARCHY_POSITION_TO_DATAID<br /><br /> RELATIONSHIP|  
|**COLUMN_ENCODING**|**DBTYPE_UI8**||表示用於資料行資料之編碼類型的整數。<br /><br /> **0**，搭配**COLUMN_TYPE**: HIERARCHY_DATAID_TO_POSITION、 HIERARCHY_POSITION_TO_DATAID、 關聯性<br /><br /> **1**，搭配**COLUMN_TYPE**: BASIC_DATA<br /><br /> **2**，搭配**COLUMN_TYPE**: BASIC_DATA|  
|**資料類型**|**DBTYPE_WSTR**||資料行的資料類型。 具有下列可能的值：<br /><br /> DBTYPE_BOOL<br /><br /> DBTYPE_CY<br /><br /> DBTYPE_DATE<br /><br /> DBTYPE_I4<br /><br /> DBTYPE_I8<br /><br /> DBTYPE_R8<br /><br /> DBTYPE_WSTR<br /><br /> 不適用|  
|**ISKEY**|**DBTYPE_BOOL**||**True**如果資料行做為主要或外部索引鍵的索引鍵使用; 否則為**false**。|  
|**ISUNIQUE**|**DBTYPE_BOOL**||**True**如果資料行中的值是唯一的否則為**false**。|  
|**ISNULLABLE**|**DBTYPE_BOOL**||**True**如果資料行可為 null，否則為**false**。|  
|**ISROWNUMBER**|**DBTYPE_BOOL**||**True**如果資料行是資料列號碼資料行。 資料列數目資料行供 xVelocity 記憶體中分析引擎內部使用。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|值|  
|--------------|-----------|  
|GUID|a07ccd44-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageTableColumns|  
  
## <a name="example"></a>範例  
 下列程式碼範例使用 DMV 查詢傳回結果集。  
  
```  
SELECT *  
FROM $System.DISCOVER_STORAGE_TABLE_COLUMNS  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 結構描述資料列集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

