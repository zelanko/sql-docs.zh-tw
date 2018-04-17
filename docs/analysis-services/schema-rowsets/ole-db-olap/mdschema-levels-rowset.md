---
title: MDSCHEMA_LEVELS 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDSCHEMA_LEVELS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_LEVELS rowset
ms.assetid: 4313e268-33f4-4e99-96d7-2ec26775c580
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7eb78b431b77dadfe216db5e30e77e9d5722b2a8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemalevels-rowset"></a>MDSCHEMA_LEVELS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述特定階層內的每個層級。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_LEVELS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|描述|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|此層級所屬目錄的名稱。 **NULL**如果提供者不支援類別目錄。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|此層級所屬結構描述的名稱。 **NULL**如果提供者不支援結構描述。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|此層級所屬 Cube 的名稱。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|此層級所屬維度的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|階層架構的唯一名稱。 如果該層級屬於多個階層，該層級所屬的每個階層都會有一個資料列。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**L**|**DBTYPE_WSTR**|層級的名稱。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|層級的正確逸出唯一名稱。|  
|**LEVEL_GUID**|**DBTYPE_GUID**|不支援。|  
|**LEVEL_CAPTION**|**DBTYPE_WSTR**|與階層關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在， **l**傳回。|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|層級距離根階層的距離。 根層級為零 (**0)**。|  
|**LEVEL_CARDINALITY**|**DBTYPE_UI4**|層級中的成員數目。|  
|**LEVEL_TYPE**|**DBTYPE_I4**|層級的類型：<br /><br /> **MDLEVEL_TYPE_GEO_CONTINENT** (**0x2001**)<br /><br /> **MDLEVEL_TYPE_GEO_REGION** (**0x2002 時**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTRY** (**0x2003**)<br /><br /> **MDLEVEL_TYPE_GEO_STATE_OR_PROVINCE** (**0x2004**)<br /><br /> **MDLEVEL_TYPE_GEO_COUNTY** (**0x2005**)<br /><br /> **MDLEVEL_TYPE_GEO_CITY** (**0x2006**)<br /><br /> **MDLEVEL_TYPE_GEO_POSTALCODE** (**0x2007**)<br /><br /> **MDLEVEL_TYPE_GEO_POINT** (**0x2008**)<br /><br /> **MDLEVEL_TYPE_ORG_UNIT** (**0x1011**)<br /><br /> **MDLEVEL_TYPE_BOM_RESOURCE** (**0x1012**)<br /><br /> **MDLEVEL_TYPE_QUANTITATIVE** (**0x1013**)<br /><br /> **MDLEVEL_TYPE_ACCOUNT** (**0x1014**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER** (**0x1021**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_GROUP** (**0x1022**)<br /><br /> **MDLEVEL_TYPE_CUSTOMER_HOUSEHOLD** (**0x1023**)<br /><br /> **MDLEVEL_TYPE_PRODUCT** (**0x1031**)<br /><br /> **MDLEVEL_TYPE_PRODUCT_GROUP** (**0x1032**)<br /><br /> **MDLEVEL_TYPE_SCENARIO** (**0x1015**)<br /><br /> **MDLEVEL_TYPE_UTILITY** (**0x1016**)<br /><br /> **MDLEVEL_TYPE_PERSON** (**0x1041**)<br /><br /> **MDLEVEL_TYPE_COMPANY** (**0x1042**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_SOURCE** (**0x1051**)<br /><br /> **MDLEVEL_TYPE_CURRENCY_DESTINATION** (**0x1052**)<br /><br /> **MDLEVEL_TYPE_CHANNEL** (**0x1061**)<br /><br /> **MDLEVEL_TYPE_REPRESENTATIVE** (**0x1062**)<br /><br /> **MDLEVEL_TYPE_PROMOTION** (**0x1071**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|層級的可讀取描述。 如果沒有描述，則為 NULL。|  
|**CUSTOM_ROLLUP_SETTINGS**|**DBTYPE_I4**|指定自訂積存選項的點陣圖：<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_EXPRESSION** (**0x01**) 指出有運算式存在此層級。 (已被取代)<br /><br /> **MDLEVELS_CUSTOM_ROLLUP_COLUMN** (**0x02**) 指出此層級的自訂積存資料行。<br /><br /> **MDLEVELS_SKIPPED_LEVELS** (**0x04**) 表示略過的層級，此層級的成員相關聯。<br /><br /> **MDLEVELS_CUSTOM_MEMBER_PROPERTIES** (**0x08**) 指出層級的成員有自訂成員屬性。<br /><br /> **MDLEVELS_UNARY_OPERATOR** (**0x10**) 指出層級的成員有一元運算子。|  
|**LEVEL_UNIQUE_SETTINGS**|**DBTYPE_I4**|點陣圖，指定當層級只擁有具有唯一名稱或索引鍵的成員時，哪些資料行包含唯一值。 Msmd.h 檔案為此點陣圖定義下列的位元值常數：<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**)<br /><br /> **MDDIMENSIONS_MEMBER_NAME_UNIQUE** (**2**)<br /><br /> <br /><br /> 請注意索引鍵一定是唯一的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 名稱會是唯一，如果屬性設定為**UniqueInDimension**或**UniqueInAttribute**|  
|**LEVEL_IS_VISIBLE**|**DBTYPE_BOOL**|布林值，指出層級是否為可見。<br /><br /> 永遠傳回 True。 如果層級為不可見，就不會包含在結構描述資料列集中。|  
|**LEVEL_ORDERING_PROPERTY**|**DBTYPE_WSTR**|層級用於排序之屬性的識別碼。|  
|**LEVEL_DBTYPE**|**DBTYPE_I4**|**DBTYPE**成員索引鍵資料行層級屬性所使用的列舉型別。<br /><br /> 如果使用串連的索引鍵做為成員索引鍵資料行，則為 Null。|  
|**LEVEL_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|一律傳回 NULL。|  
|**LEVEL_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|層級成員名稱的 SQL 表示法。|  
|**LEVEL_KEY_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|層級成員索引鍵值的 SQL 表示法。|  
|**LEVEL_UNIQUE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**|成員唯一名稱的 SQL 表示法。|  
|**LEVEL_ATTRIBUTE_HIERARCHY_NAME**|**DBTYPE_WSTR**|提供層級來源之屬性階層的名稱。|  
|**LEVEL_KEY_CARDINALITY**|**DBTYPE_UI2**|層級索引鍵中的資料行數。|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|定義層級來源的點陣圖：<br /><br /> **MD_ORIGIN_USER_DEFINED**識別使用者定義階層中的層級。<br /><br /> **MD_ORIGIN_ATTRIBUTE**識別屬性階層的層級。<br /><br /> **MD_ORIGIN_KEY_ATTRIBUTE**識別索引鍵屬性階層的層級。<br /><br /> **MD_ORIGIN_INTERNAL**識別未啟用屬性階層中的層級。|  
  
 排序資料列集**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **DIMENSION_UNIQUE_NAME**， **HIERARCHY_UNIQUE_NAME**， **LEVEL_NUMBER**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_LEVELS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**L**|**DBTYPE_WSTR**|選擇性。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**LEVEL_ORIGIN**|**DBTYPE_UI2**|（選擇性）預設限制會在作用中**MD_USER_DEFINED**和**MD_SYSTEM_ENABLED**|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION (維度)|  
|**LEVEL_VISIBILITY**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 使用下列值之一的點陣圖：<br /><br /> 1 可見<br /><br /> 2 不可見|  
  
## <a name="see-also"></a>請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
