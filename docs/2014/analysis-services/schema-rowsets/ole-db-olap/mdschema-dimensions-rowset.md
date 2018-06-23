---
title: MDSCHEMA_DIMENSIONS 資料列集 |Microsoft 文件
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
- MDSCHEMA_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b00b617adf90e1dba8eac94a9872ce07c0773e7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030172"
---
# <a name="mdschemadimensions-rowset"></a>MDSCHEMA_DIMENSIONS 資料列集
  描述資料庫內的共用和私人維度。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_DIMENSIONS` 資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||資料庫的名稱。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Cube 的名稱。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||維度的名稱。 如果維度是一個以上 Cube 或量值群組的部分，則每個維度、維度群組和 Cube 的唯一組合會有一個資料列。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||維度的唯一名稱。|  
|`DIMENSION_GUID`|`DBTYPE_GUID`||不支援。|  
|`DIMENSION_CAPTION`|`DBTYPE_WSTR`||維度的標題。 這會用於顯示維度名稱給使用者時，例如在使用者介面或報表中。|  
|`DIMENSION_ORDINAL`|`DBTYPE_UI4`||Cube 內維度的位置。|  
|`DIMENSION_TYPE`|`DBTYPE_I2`||維度的類型。 有效值包括：<br /><br /> -   `MD_DIMTYPE_UNKNOWN` (`0`)<br />-   `MD_DIMTYPE_TIME` (`1`)<br />-   `MD_DIMTYPE_MEASURE` (`2`)<br />-   `MD_DIMTYPE_OTHER` (`3`)<br />-   `MD_DIMTYPE_QUANTITATIVE` (`5`)<br />-   `MD_DIMTYPE_ACCOUNTS` (`6`)<br />-   `MD_DIMTYPE_CUSTOMERS` (`7`)<br />-   `MD_DIMTYPE_PRODUCTS` (`8`)<br />-   `MD_DIMTYPE_SCENARIO` (`9`)<br />-   `MD_DIMTYPE_UTILIY` (`10`)<br />-   `MD_DIMTYPE_CURRENCY` (`11`)<br />-   `MD_DIMTYPE_RATES` (`12`)<br />-   `MD_DIMTYPE_CHANNEL` (`13`)<br />-   `MD_DIMTYPE_PROMOTION` (`14`)<br />-   `MD_DIMTYPE_ORGANIZATION` (`15`)<br />-   `MD_DIMTYPE_BILL_OF_MATERIALS` (`16`)<br />-   `MD_DIMTYPE_GEOGRAPHY` (`17`)|  
|`DIMENSION_CARDINALITY`|`DBTYPE_UI4`||索引鍵屬性中的成員數目。|  
|`DEFAULT_HIERARCHY`|`DBTYPE_WSTR`||維度的階層。 保留這個項目的目的，是為了與舊版相容。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||維度的易記描述。|  
|`IS_VIRTUAL`|`DBTYPE_BOOL`||永遠都是 `FALSE`。|  
|`IS_READWRITE`|`DBTYPE_BOOL`||布林值，指出維度是否為可寫入。<br /><br /> 如果維度為可寫入的，則為 `TRUE`。|  
|`DIMENSION_UNIQUE_SETTINGS`|`DBTYPE_I4`||點陣圖，指定當維度只擁有具有唯一名稱的成員時，哪些資料行包含唯一值。 下列位元值常數會針對此點陣圖定義於 Msmd.h：<br /><br /> -   `MDDIMENSIONS_MEMBER_KEY_UNIQUE`|  
|`DIMENSION_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||永遠都是 `NULL`。|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||永遠都是 `TRUE`。 **注意：** 維度除非維度中的一個或多個階層都會顯示為不可見。|  
  
 資料列集會按 `CATALOG_NAME`、`SCHEMA_NAME`、`CUBE_NAME` 和 `DIMENSION_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_DIMENSIONS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 的 CUBE<br />-2 的維度<br /><br /> 預設限制為值 1。|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 看得見<br />-2 不可見<br /><br /> 預設限制為值 1。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  