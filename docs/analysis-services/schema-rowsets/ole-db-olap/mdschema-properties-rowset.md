---
title: "MDSCHEMA_PROPERTIES 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_PROPERTIES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_PROPERTIES rowset
ms.assetid: 95c480f7-c525-44ba-a59b-cd36f5855a4f
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 13c187e2620c825f70a20637ab1fffb8560dbd1a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemaproperties-rowset"></a>MDSCHEMA_PROPERTIES 資料列集
  描述資料庫內的成員屬性。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_PROPERTIES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||資料庫的名稱。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||此屬性所屬的結構描述名稱。 **NULL**如果提供者不支援結構描述。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Cube 的名稱。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||維度的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||階層架構的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||此屬性所屬層級的唯一名稱。 如果提供者不支援具名層級，它應該傳回**DIMENSION_UNIQUE_NAME**這個欄位的值。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||屬性所屬成員的唯一名稱。 用於不支援具名層級或具有每個成員之屬性的資料存放區。 該屬性適用於層級中的所有成員，這個資料行是否為**NULL**。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**PROPERTY_TYPE**|**DBTYPE_I2**||點陣圖，指出屬性的類型。<br /><br /> **MDPROP_MEMBER** (**1**) 識別成員的屬性。 此屬性可用於 SELECT 陳述式的 DIMENSION PROPERTIES 子句中。<br /><br /> **MDPROP_CELL** (**2**) 識別的資料格屬性。 此屬性可用於 SELECT 陳述式結尾的 CELL PROPERTIES 子句中。<br /><br /> **MDPROP_SYSTEM** (**4**) 識別內部屬性。<br /><br /> **MDPROP_BLOB** (**8**) 識別用來包含二進位大型物件 (blob) 的屬性。|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**||屬性的名稱。 如果屬性的索引鍵的屬性名稱相同**PROPERTY_NAME**會是空白。|  
|**PROPERTY_CAPTION**|**DBTYPE_WSTR**||與主要用於顯示目的之屬性相關聯的標籤或標題。 傳回**PROPERTY_NAME**如果標題不存在。|  
|**DATA_TYPE**|**DBTYPE_UI2**||屬性的資料型別。|  
|**CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||屬性的最大可能長度 (如果該屬性為字元、二進位或位元類型)。<br /><br /> 零代表沒有任何已定義的最大長度。<br /><br /> 傳回**NULL**對於所有其他資料類型。|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||屬性的最大可能長度 (以位元組計算) (如果該屬性為字元或二進位類型)。<br /><br /> 零代表沒有任何已定義的最大長度。<br /><br /> 傳回**NULL**對於所有其他資料類型。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||如果是數值資料類型，則為屬性的最大有效位數。<br /><br /> 傳回**NULL**對於所有其他資料類型。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||數字的小數點，如果它是右邊數目**DBTYPE_NUMERIC**或**DBTYPE_DECIMAL**型別。<br /><br /> 傳回**NULL**對於所有其他資料類型。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||人們可讀取的屬性描述。 **NULL**如果沒有描述。|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**||屬性的類型。 可以是下列其中一個列舉：<br /><br /> **MD_PROPTYPE_REGULAR** (**0x00**)<br /><br /> **MD_PROPTYPE_ID** (**0x01**)<br /><br /> **MD_PROPTYPE_RELATION_TO_PARENT** (**0x02**)<br /><br /> **MD_PROPTYPE_ROLLUP_OPERATOR** (**0x03**)<br /><br /> **MD_PROPTYPE_ORG_TITLE** (**0x11**)<br /><br /> **MD_PROPTYPE_CAPTION** (**0x21**)<br /><br /> **MD_PROPTYPE_CAPTION_SHORT** (**0x22**)<br /><br /> **MD_PROPTYPE_CAPTION_DESCRIPTION** (**0x23**)<br /><br /> **MD_PROPTYPE_CAPTION_ABREVIATION** (**0x24**)<br /><br /> **MD_PROPTYPE_WEB_URL** (**0x31**)<br /><br /> **MD_PROPTYPE_WEB_HTML** (**0x32**)<br /><br /> **MD_PROPTYPE_WEB_XML_OR_XSL** (**0x33**)<br /><br /> **MD_PROPTYPE_WEB_MAIL_ALIAS** (**0x34**)<br /><br /> **MD_PROPTYPE_ADDRESS** (**0x41**)<br /><br /> **MD_PROPTYPE_ADDRESS_STREET** (**0x42**)<br /><br /> **MD_PROPTYPE_ADDRESS_HOUSE** (**0x43**)<br /><br /> **MD_PROPTYPE_ADDRESS_CITY** (**0x44**)<br /><br /> **MD_PROPTYPE_ADDRESS_STATE_OR_PROVINCE** (**0x45**)<br /><br /> **MD_PROPTYPE_ADDRESS_ZIP** (**0x46**)<br /><br /> **MD_PROPTYPE_ADDRESS_QUARTER** (**0x47**)<br /><br /> **MD_PROPTYPE_ADDRESS_COUNTRY** (**方式 0x48**)<br /><br /> **MD_PROPTYPE_ADDRESS_BUILDING** (**方式 0x49**)<br /><br /> **MD_PROPTYPE_ADDRESS_ROOM** (**0x4A**)<br /><br /> **MD_PROPTYPE_ADDRESS_FLOOR** (**0x4b 放**)<br /><br /> **MD_PROPTYPE_ADDRESS_FAX** (**0x4C**)<br /><br /> **MD_PROPTYPE_ADDRESS_PHONE** (**0x4D**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_X** (**0x61**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Y** (**0x62**)<br /><br /> **MD_PROPTYPE_GEO_CENTROID_Z** (**0x63**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_TOP** (**0x64**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_LEFT** (**0x65**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_BOTTOM** (**0x66**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_RIGHT** (**0x67**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_FRONT** (**0x68**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_REAR** (**0x69**)<br /><br /> **MD_PROPTYPE_GEO_BOUNDARY_POLYGON** (**0x6A**)<br /><br /> **MD_PROPTYPE_PHYSICAL_SIZE** (**0x71**)<br /><br /> **MD_PROPTYPE_PHYSICAL_COLOR** (**0x72**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WEIGHT** (**0x73**)<br /><br /> **MD_PROPTYPE_PHYSICAL_HEIGHT** (**0x74**)<br /><br /> **MD_PROPTYPE_PHYSICAL_WIDTH** (**0x75**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DEPTH** (**0x76**)<br /><br /> **MD_PROPTYPE_PHYSICAL_VOLUME** (**0x77**)<br /><br /> **MD_PROPTYPE_PHYSICAL_DENSITY** (**0x78**)<br /><br /> **MD_PROPTYPE_PERSON_FULL_NAME** (**0x82**)<br /><br /> **MD_PROPTYPE_PERSON_FIRST_NAME** (**0x83**)<br /><br /> **MD_PROPTYPE_PERSON_LAST_NAME** (**0x84**)<br /><br /> **MD_PROPTYPE_PERSON_MIDDLE_NAME** (**0x85**)<br /><br /> **MD_PROPTYPE_PERSON_DEMOGRAPHIC** (**0x86**)<br /><br /> **MD_PROPTYPE_PERSON_CONTACT** (**0x87**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_LOW** (**0x91**)<br /><br /> **MD_PROPTYPE_QTY_RANGE_HIGH** (**0x92**)<br /><br /> **MD_PROPTYPE_FORMATTING_COLOR** (**0xA1**)<br /><br /> **MD_PROPTYPE_FORMATTING_ORDER** (**0xA2**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT** (**0xA3**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_EFFECTS** (**0xA4**)<br /><br /> **MD_PROPTYPE_FORMATTING_FONT_SIZE** (**0xA5**)<br /><br /> **MD_PROPTYPE_FORMATTING_SUB_TOTAL** (**0xA6**)<br /><br /> **MD_PROPTYPE_DATE** (**0xB1**)<br /><br /> **MD_PROPTYPE_DATE_START** (**0xB2**)<br /><br /> **MD_PROPTYPE_DATE_ENDED** (**0xB3**)<br /><br /> **MD_PROPTYPE_DATE_CANCELED** (**0xB4**)<br /><br /> **MD_PROPTYPE_DATE_MODIFIED** (**0xB5**)<br /><br /> **MD_PROPTYPE_DATE_DURATION** (**0xB6**)<br /><br /> **MD_PROPTYPE_VERSION** (**0xC1**)|  
|**SQL_COLUMN_NAME**|**DBTYPE_WSTR**||SQL 查詢從 Cube 維度或資料庫 dDimension 所使用的屬性名稱。|  
|**LANGUAGE**|**DBTYPE_UI2**||轉譯表示為**LCID**。 只適用於屬性翻譯。|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**||識別屬性所套用至的階層類型：<br /><br /> **MD_USER_DEFINED** (**1**) 指出此屬性位於使用者定義階層<br /><br /> **MD_SYSTEM_ENABLED** (**2**) 指出屬性階層上的屬性<br /><br /> **MD_SYSTEM_DISABLED** (**4**) 指出屬性位在未啟用屬性階層。|  
|**PROPERTY_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**||此屬性 (Property) 來源之屬性 (Attribute) 階層的名稱。|  
|**PROPERTY_CARDINALITY**|**DBTYPE_WSTR**||屬性的基數。 可能的值包括下列字串：<br /><br /> **其中一個**<br /><br /> **許多**|  
|**MIME_TYPE**|**DBTYPE_WSTR**||二進位大型物件 (BLOB) 的 MIME 類型。|  
|**PROPERTY_IS_VISIBLE**|**DBTYPE_BOOL**||布林值，指出屬性是否為可見。<br /><br /> **TRUE**如果屬性為可見，否則**FALSE**。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_PROPERTIES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|強制性|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**PROPERTY_TYPE**|**DBTYPE_I2**|選擇性|  
|**PROPERTY_NAME**|**DBTYPE_WSTR**|選擇性|  
|**PROPERTY_CONTENT_TYPE**|**DBTYPE_I2**|（選擇性）預設限制會放在**MDPROP_MEMBER**或者**MDPROP_CELL**。|  
|**PROPERTY_ORIGIN**|**DBTYPE_UI2**|（選擇性）預設限制會放在**MD_USER_DEFINED**或者**MD_SYSTEM_ENABLED**。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。  點陣圖，下列有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION (維度)|  
|**PROPERTY_VISIBILITY**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 可見<br /><br /> 2 不可見|  
  
## <a name="see-also"></a>請參閱＜  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
