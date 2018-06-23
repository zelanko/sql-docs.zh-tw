---
title: MDSCHEMA_MEASUREGROUP_DIMENSIONS 資料列集 |Microsoft 文件
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
api_name:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUP_DIMENSIONS rowset
ms.assetid: c731c06a-7382-4e50-ba0e-d8cee3ab4f28
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f607b966099f71acee460a5a343c557e2a81857e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031722"
---
# <a name="mdschemameasuregroupdimensions-rowset"></a>MDSCHEMA_MEASUREGROUP_DIMENSIONS 資料列集
  列舉量值群組的維度。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_MEASUREGROUP_DIMENSIONS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此量值群組所屬目錄的名稱。 如果提供者不支援目錄，則為 `NULL`。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此量值群組所屬 Cube 的名稱。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||量值群組的名稱。|  
|`MEASUREGROUP_CARDINALITY`|`DBTYPE_WSTR`||量值群組中的量值針對單一維度成員所可能擁有的執行個體數目。 可能的值包括：<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||維度的唯一名稱。|  
|`DIMENSION_CARDINALITY`|`DBTYPE_WSTR`||維度成員針對量值群組量值的單一執行個體所可能擁有的執行個體數目。<br /><br /> 可能的值包括：<br /><br /> -   `ONE`<br />-   `MANY`|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||布林值，指出維度中的階層是否為可見。<br /><br /> 如果維度中有一個或多個階層為可見的，則傳回 `TRUE`，否則傳回 `FALSE`。|  
|`DIMENSION_IS_FACT_DIMENSION`|`DBTYPE_BOOL`||布林值，指出維度是否為事實維度。<br /><br /> 如果維度是事實維度，則傳回 `TRUE`，否則傳回 `FALSE`。|  
|`DIMENSION_PATH`|`DBTYPE_HCHAPTER`||參考維度的維度清單。|  
|`DIMENSION_GRANULARITY`|`DBTYPE_WSTR`||資料粒度階層的唯一名稱。|  
  
 資料列集支援按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME`、`MEASUREGROUP_NAME` 和 `DIMENSION_UNIQUE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_MEASUREGROUP_DIMENSIONS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 看得見<br />-2 不可見<br />預設限制為 1 的值。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  