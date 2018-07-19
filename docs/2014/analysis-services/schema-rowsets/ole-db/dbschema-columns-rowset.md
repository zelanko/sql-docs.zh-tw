---
title: DBSCHEMA_COLUMNS 資料列集 |Microsoft Docs
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
api_name:
- DBSCHEMA_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6fa933eb153b0d8de4c2fec4ba92b072954be141
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267574"
---
# <a name="dbschemacolumns-rowset"></a>DBSCHEMA_COLUMNS 資料列集
  為所有符合提供之限制準則的資料行提供資料行資訊。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DBSCHEMA_COLUMNS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`||資料庫的名稱。|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`||不支援。|  
|`TABLE_NAME`|`DBTYPE_WSTR`||Cube 的名稱。|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||屬性階層或量值的名稱。|  
|`COLUMN_GUID`|`DBTYPE_GUID`||不支援。|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||不支援。|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||以 1 為開頭的資料行位置。|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||不支援。|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||不支援。|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||指出資料行屬性的 `DBCOLUMNFLAGS` 位元遮罩。 在 請參閱 < DBCOLUMNFLAGS 列舉類型' [icolumnsinfo:: Getcolumninfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||一律會傳回`false`。|  
|`DATA_TYPE`|`DBTYPE_WSTR`<br /><br /> `DBTYPE_VARIANT`||資料行的資料類型。 傳回維度資料行的字串以及量值的變數。|  
|`TYPE_GUID`|`DBTYPE_GUID`||不支援。|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||資料行中值的最大可能長度。<br /><br /> 這是從 `DataSize` 的 `DataItem` 屬性擷取的。|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||針對字元或是二進位資料行，資料行中值的最大可能長度 (以位元組為單位)。<br /><br /> 值為零 (0) 表示資料行沒有最大長度限制。<br /><br /> 對於沒有傳回二進位或是字元資料類型的資料行，將傳回 `NULL`。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||`DBTYPE_VARNUMERIC` 以外的數值資料類型之資料行的最大精確度。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||`DBTYPE_DECIMAL`、`DBTYPE_NUMERIC`、`DBTYPE_VARNUMERIC` 小數點右邊的位數。 否則，這個值為 `NULL`。|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||不支援。|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||不支援。|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||不支援。|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||不支援。|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||不支援。|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||不支援。|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||不支援。|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||不支援。|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||不支援。|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||不支援。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||不支援。|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`||物件的 OLAP 類型。<br /><br /> `MEASURE` 指出物件是量值。<br /><br /> `ATTRIBUTE` 指出物件是維度屬性。<br /><br /> `SCHEMA` 表示物件是結構描述中的資料行。|  
  
 資料列集會在 `TABLE_CATALOG`、`TABLE_SCHEMA` 和 `TABLE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DBSCHEMA_COLUMNS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|選擇性|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|選擇性|  
|`TABLE_NAME`|`DBTYPE_WSTR`|選擇性|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|選擇性|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`|選擇性|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 結構描述資料列集](ole-db-schema-rowsets.md)  
  
  
