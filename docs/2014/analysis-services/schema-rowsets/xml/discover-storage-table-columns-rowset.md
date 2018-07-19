---
title: DISCOVER_STORAGE_TABLE_COLUMNS 資料列集 |Microsoft Docs
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
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e480f60aa857506a1d192452b299cede3f7161e5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153149"
---
# <a name="discoverstoragetablecolumns-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMNS 資料列集
  提供在資料行層級中，有關 SharePoint 或表格式模式下執行 Analysis Services 資料庫所用儲存體資料表的資訊。  
  
 **適用於：** 表格式模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_STORAGE_TABLE_COLUMNS`資料列集包含下列資料行。  
  
|**資料行名稱**|**類型指標**|**限制**|**說明**|  
|---------------------|------------------------|---------------------|---------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|是|指定包含資料表的資料庫名稱。 如果省略，就會使用目前的資料庫。<br /><br /> `DISCOVER_STORAGE_TABLE_COLUMNS`使用此資料行也可以限制資料列集。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|是|指定包含資料表的 Cube 或模型。<br /><br /> `DISCOVER_STORAGE_TABLES`使用此資料行也可以限制資料列集。|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|是|量值群組的名稱。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||維度的名稱。|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||屬性的名稱。|  
|`TABLE_ID`|`DBTYPE_WSTR`||資料表的識別碼。|  
|`COLUMN_ID`|`DBTYPE_ WSTR`||資料行的識別碼。 資料行識別碼是 xVelocity 記憶體中分析引擎 (VertiPaq) 內部的識別碼，因此，僅提供資訊之用。|  
|`COLUMN_TYPE`|`DBTYPE_WSTR`||資料行的類型。 資料行類型是 xVelocity 記憶體中分析引擎 (VertiPaq) 內部的類型，因此，僅提供資訊之用。<br /><br /> -BASIC_DATA<br />-HIERARCHY_DATAID_TO_POSITION<br />-HIERARCHY_POSITION_TO_DATAID<br />-關聯性|  
|`COLUMN_ENCODING`|`DBTYPE_UI8`||表示用於資料行資料之編碼類型的整數。<br /><br /> -   **0**，搭配`COLUMN_TYPE`: HIERARCHY_DATAID_TO_POSITION、 HIERARCHY_POSITION_TO_DATAID、 關聯性<br />-   **1**，搭配`COLUMN_TYPE`: BASIC_DATA<br />-   **2**，搭配`COLUMN_TYPE`: BASIC_DATA|  
|`DATATYPE`|`DBTYPE_WSTR`||資料行的資料類型。 具有下列可能的值：<br /><br /> -DBTYPE_BOOL<br />-DBTYPE_CY<br />-DBTYPE_DATE<br />-DBTYPE_I4<br />-DBTYPE_I8<br />-DBTYPE_R8<br />-DBTYPE_WSTR<br />-N/A|  
|`ISKEY`|`DBTYPE_BOOL`||如果資料行當做主要或外部索引鍵使用，則為 `True`，否則為 `false`。|  
|`ISUNIQUE`|`DBTYPE_BOOL`||如果資料行中的值是唯一的，則為 `True`，否則為 `false`。|  
|`ISNULLABLE`|`DBTYPE_BOOL`||如果資料行可為 Null，則為 `True`，否則為 `false`。|  
|`ISROWNUMBER`|`DBTYPE_BOOL`||如果資料行是資料列號碼資料行，則為 `True`。 資料列數目資料行供 xVelocity 記憶體中分析引擎內部使用。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
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
 [Analysis Services 結構描述資料列集](../analysis-services-schema-rowsets.md)  
  
  
