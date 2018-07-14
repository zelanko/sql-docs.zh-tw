---
title: MDSCHEMA_PROPERTIES 資料列集 |Microsoft Docs
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
- MDSCHEMA_PROPERTIES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f62a6e4f77053c1aec69fc2e16b8049193249466
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189215"
---
# <a name="mdschemaproperties-rowset"></a>MDSCHEMA_PROPERTIES 資料列集
  描述資料庫內的成員屬性。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_PROPERTIES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||資料庫的名稱。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||此屬性所屬的結構描述名稱。 如果提供者不支援結構描述，則為 `NULL`。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Cube 的名稱。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||維度的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||階層架構的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||此屬性所屬層級的唯一名稱。 如果提供者不支援具名層級，則應該傳回此欄位的 `DIMENSION_UNIQUE_NAME` 值。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||屬性所屬成員的唯一名稱。 用於不支援具名層級或具有每個成員之屬性的資料存放區。 如果屬性適用於層級中的所有成員，則此資料行為 `NULL`。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|`PROPERTY_TYPE`|`DBTYPE_I2`||點陣圖，指出屬性的類型。<br /><br /> -   `MDPROP_MEMBER` (`1`) 識別成員的屬性。 此屬性可用於 SELECT 陳述式的 DIMENSION PROPERTIES 子句中。<br />-   `MDPROP_CELL` (`2`) 識別的資料格屬性。 此屬性可用於 SELECT 陳述式結尾的 CELL PROPERTIES 子句中。<br />-   `MDPROP_SYSTEM` (`4`) 識別內部屬性。<br />-   `MDPROP_BLOB` (`8`) 識別包含二進位大型物件 (blob) 的屬性。|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`||屬性的名稱。 如果屬性的索引鍵與屬性的名稱相同，則 `PROPERTY_NAME` 會是空白的。|  
|`PROPERTY_CAPTION`|`DBTYPE_WSTR`||與主要用於顯示目的之屬性相關聯的標籤或標題。 如果標題不存在，則傳回 `PROPERTY_NAME`。|  
|`DATA_TYPE`|`DBTYPE_UI2`||屬性的資料型別。|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||屬性的最大可能長度 (如果該屬性為字元、二進位或位元類型)。<br /><br /> 零代表沒有任何已定義的最大長度。<br /><br /> 如果是所有其他的資料類型，就會傳回 `NULL`。|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||屬性的最大可能長度 (以位元組計算) (如果該屬性為字元或二進位類型)。<br /><br /> 零代表沒有任何已定義的最大長度。<br /><br /> 如果是所有其他的資料類型，就會傳回 `NULL`。|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||如果是數值資料類型，則為屬性的最大有效位數。<br /><br /> 如果是所有其他的資料類型，就會傳回 `NULL`。|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||小數點右邊的位數 (如果小數點是 `DBTYPE_NUMERIC` 或 `DBTYPE_DECIMAL` 類型)。<br /><br /> 如果是所有其他的資料類型，就會傳回 `NULL`。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||人們可讀取的屬性描述。 如果沒有描述，則為 `NULL`。|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`||屬性的類型。 可以是下列其中一個列舉：<br /><br /> -   **MD_PROPTYPE_REGULAR** (`0x00`)<br />-   **MD_PROPTYPE_ID** (`0x01`)<br />-   **MD_PROPTYPE_RELATION_TO_PARENT** (`0x02`)<br />-   **MD_PROPTYPE_ROLLUP_OPERATOR** (`0x03`)<br />-   **MD_PROPTYPE_ORG_TITLE** (`0x11`)<br />-   **MD_PROPTYPE_CAPTION** (`0x21`)<br />-   **MD_PROPTYPE_CAPTION_SHORT** (`0x22`)<br />-   **MD_PROPTYPE_CAPTION_DESCRIPTION** (`0x23`)<br />-   **MD_PROPTYPE_CAPTION_ABREVIATION** (`0x24`)<br />-   **MD_PROPTYPE_WEB_URL** (`0x31`)<br />-   **MD_PROPTYPE_WEB_HTML** (`0x32`)<br />-   **MD_PROPTYPE_WEB_XML_OR_XSL** (`0x33`)<br />-   **MD_PROPTYPE_WEB_MAIL_ALIAS** (`0x34`)<br />-   **MD_PROPTYPE_ADDRESS** (`0x41`)<br />-   **MD_PROPTYPE_ADDRESS_STREET** (`0x42`)<br />-   **MD_PROPTYPE_ADDRESS_HOUSE** (`0x43`)<br />-   **MD_PROPTYPE_ADDRESS_CITY** (`0x44`)<br />-   **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (`0x45`)<br />-   **MD_PROPTYPE_ADDRESS_ZIP** (`0x46`)<br />-   **MD_PROPTYPE_ADDRESS_QUARTER** (`0x47`)<br />-   **MD_PROPTYPE_ADDRESS_COUNTRY** (`0x48`)<br />-   **MD_PROPTYPE_ADDRESS_BUILDING** (`0x49`)<br />-   **MD_PROPTYPE_ADDRESS_ROOM** (`0x4A`)<br />-   **MD_PROPTYPE_ADDRESS_FLOOR** (`0x4B`)<br />-   **MD_PROPTYPE_ADDRESS_FAX** (`0x4C`)<br />-   **MD_PROPTYPE_ADDRESS_PHONE** (`0x4D`)<br />-   **MD_PROPTYPE_GEO_CENTROID_X** (`0x61`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Y** (`0x62`)<br />-   **MD_PROPTYPE_GEO_CENTROID_Z** (`0x63`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_TOP** (`0x64`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (`0x65`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (`0x66`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (`0x67`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (`0x68`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_REAR** (`0x69`)<br />-   **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (`0x6A`)<br />-   **MD_PROPTYPE_PHYSICAL_SIZE** (`0x71`)<br />-   **MD_PROPTYPE_PHYSICAL_COLOR** (`0x72`)<br />-   **MD_PROPTYPE_PHYSICAL_WEIGHT** (`0x73`)<br />-   **MD_PROPTYPE_PHYSICAL_HEIGHT** (`0x74`)<br />-   **MD_PROPTYPE_PHYSICAL_WIDTH** (`0x75`)<br />-   **MD_PROPTYPE_PHYSICAL_DEPTH** (`0x76`)<br />-   **MD_PROPTYPE_PHYSICAL_VOLUME** (`0x77`)<br />-   **MD_PROPTYPE_PHYSICAL_DENSITY** (`0x78`)<br />-   **MD_PROPTYPE_PERSON_FULL_NAME** (`0x82`)<br />-   **MD_PROPTYPE_PERSON_FIRST_NAME** (`0x83`)<br />-   **MD_PROPTYPE_PERSON_LAST_NAME** (`0x84`)<br />-   **MD_PROPTYPE_PERSON_MIDDLE_NAME** (`0x85`)<br />-   **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (`0x86`)<br />-   **MD_PROPTYPE_PERSON_CONTACT** (`0x87`)<br />-   **MD_PROPTYPE_QTY_RANGE_LOW** (`0x91`)<br />-   **MD_PROPTYPE_QTY_RANGE_HIGH** (`0x92`)<br />-   **MD_PROPTYPE_FORMATTING_COLOR** (`0xA1`)<br />-   **MD_PROPTYPE_FORMATTING_ORDER** (`0xA2`)<br />-   **MD_PROPTYPE_FORMATTING_FONT** (`0xA3`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (`0xA4`)<br />-   **MD_PROPTYPE_FORMATTING_FONT_SIZE** (`0xA5`)<br />-   **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (`0xA6`)<br />-   **MD_PROPTYPE_DATE** (`0xB1`)<br />-   **MD_PROPTYPE_DATE_START** (`0xB2`)<br />-   **MD_PROPTYPE_DATE_ENDED** (`0xB3`)<br />-   **MD_PROPTYPE_DATE_CANCELED** (`0xB4`)<br />-   **MD_PROPTYPE_DATE_MODIFIED** (`0xB5`)<br />-   **MD_PROPTYPE_DATE_DURATION** (`0xB6`)<br />-   **MD_PROPTYPE_VERSION** (`0xC1`)|  
|`SQL_COLUMN_NAME`|`DBTYPE_WSTR`||SQL 查詢從 Cube 維度或資料庫 dDimension 所使用的屬性名稱。|  
|`LANGUAGE`|`DBTYPE_UI2`||表示為 `LCID` 的翻譯。 只適用於屬性翻譯。|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`||識別屬性所套用至的階層類型：<br /><br /> -   `MD_USER_DEFINED` (`1`) 指出此屬性位於使用者定義階層<br />-   `MD_SYSTEM_ENABLED` (`2`) 指出屬性階層上的屬性<br />-   `MD_SYSTEM_DISABLED` (`4`) 指出屬性是在未啟用屬性階層。|  
|`PROPERTY_ATTRIBUTE_HIERARCHY_NAME`|`DBTYPE_WSTR`||此屬性 (Property) 來源之屬性 (Attribute) 階層的名稱。|  
|`PROPERTY_CARDINALITY`|`DBTYPE_WSTR`||屬性的基數。 可能的值包括下列字串：<br /><br /> -   `ONE`<br />-   `MANY`|  
|`MIME_TYPE`|`DBTYPE_WSTR`||二進位大型物件 (BLOB) 的 MIME 類型。|  
|`PROPERTY_IS_VISIBLE`|`DBTYPE_BOOL`||布林值，指出屬性是否為可見。<br /><br /> 如果屬性是可見的，則為 `TRUE`，否則為 `FALSE`。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_PROPERTIES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|強制性|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性|  
|`PROPERTY_TYPE`|`DBTYPE_I2`|選擇性|  
|`PROPERTY_NAME`|`DBTYPE_WSTR`|選擇性|  
|`PROPERTY_CONTENT_TYPE`|`DBTYPE_I2`|(選擇性) 預設限制會放在 `MDPROP_MEMBER` 或 `MDPROP_CELL` 上。|  
|`PROPERTY_ORIGIN`|`DBTYPE_UI2`|(選擇性) 預設限制會放在 `MD_USER_DEFINED` 或 `MD_SYSTEM_ENABLED` 上。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 的 CUBE<br />-2 的維度<br /><br /> 預設限制為值 1。|  
|`PROPERTY_VISIBILITY`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 看得見<br />-2 不可見<br /><br /> 預設限制為值 1。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  
