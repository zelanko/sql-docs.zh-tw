---
title: "MDSCHEMA_HIERARCHIES 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
apiname: MDSCHEMA_HIERARCHIES
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_HIERARCHIES rowset
ms.assetid: 2e5b2a81-366e-4d5b-af1e-1d372bf596d9
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae8601e87517fde3dbc73a080f9b3a0f85ca6a89
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemahierarchies-rowset"></a>MDSCHEMA_HIERARCHIES 資料列集
  描述特定維度中的每個階層。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_HIERARCHIES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|這個階層所屬之目錄的名稱。 **NULL**如果提供者不支援類別目錄。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不支援|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(必要項) 此階層所屬 Cube 的名稱。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|此階層所屬維度的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|階層的名稱。 如果維度中只有單一階層則為空白。 一定會有值， [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|階層架構的唯一名稱。|  
|**HIERARCHY_GUID**|**DBTYPE_GUID**|不支援|  
|**HIERARCHY_CAPTION**|**DBTYPE_WSTR**|與階層關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在， **HIERARCHY_NAME**傳回。 如果維度不包含階層或只具有一個階層，則此資料行會包含維度名稱。|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|維度的類型。 有效值包括下列各值：<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**HIERARCHY_CARDINALITY**|**DBTYPE_UI4**|階層中的成員數目。|  
|**DEFAULT_MEMBER**|**DBTYPE_WSTR**|此階層的預設成員。 這是唯一的名稱。 每個階層都必須有一個預設成員。|  
|**ALL_MEMBER**|**DBTYPE_WSTR**|積存最高層級的成員。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|人們可讀取的階層描述。 **NULL**如果沒有描述。|  
|**結構**|**DBTYPE_I2**|階層的結構。 有效值包括下列各值：<br /><br /> **MD_STRUCTURE_FULLYBALANCED** (**0**)<br /><br /> **MD_STRUCTURE_RAGGEDBALANCED** (**1**)<br /><br /> **MD_STRUCTURE_UNBALANCED** (**2**)<br /><br /> **MD_STRUCTURE_NETWORK** (**3**)|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|一律傳回**False**。|  
|**IS_READWRITE**|**DBTYPE_BOOL**|布林值，指出是否啟用回寫至維度資料行功能。<br /><br /> 傳回**TRUE**如果**回寫至維度**啟用代表此階層的資料行。|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|一律傳回**MDDIMENSIONS_MEMBER_KEY_UNIQUE** (**1**)。|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|一律傳回**NULL**。|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|一律傳回**true**。 如果維度為不可見，就不會顯示在結構描述資料列集中。|  
|**HIERARCHY_ORDINAL**|**DBTYPE_UI4**|階層在 Cube 所有階層中的序數。|  
|**DIMENSION_IS_SHARED**|**DBTYPE_BOOL**|一律傳回**TRUE**。|  
|**HIERARCHY_IS_VISIBLE**|**DBTYPE_BOOL**|布林值，指出階層是否為可見。<br /><br /> 傳回**TRUE**如果階層為可見，否則**FALSE**。|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|位元遮罩，決定階層的來源：<br /><br /> **MD_USER_DEFINED**識別使用者定義階層，而且值為**0x0000001**。<br /><br /> **MD_SYSTEM_ENABLED**識別屬性階層，且具有值為**0x0000002**。<br /><br /> **MD_SYSTEM_INTERNAL**沒有屬性階層，以識別屬性和值為**0x0000004**。<br /><br /> <br /><br /> 請注意，父子式屬性階層，是同時**MD_USER_DEFINED**和**MD_SYSTEM_ENABLED**。|  
|**HIERARCHY_DISPLAY_FOLDER**|**DBTYPE_WSTR**|在使用者介面中顯示階層時所使用的路徑。 資料夾名稱將以分號 (;) 分隔。 巢狀的資料夾會以反斜線 (\\)。|  
|**INSTANCE_SELECTION**|**DBTYPE_UI2**|提供給用戶端應用程式有關如何顯示階層的提示。 有效值包括下列各值：<br /><br /> **MD_INSTANCE_SELECTION_NONE**<br /><br /> **MD_INSTANCE_SELECTION_DROPDOWN**<br /><br /> **MD_INSTANCE_SELECTION_LIST**<br /><br /> **MD_INSTANCE_SELECTION_FILTEREDLIST**<br /><br /> **MD_INSTANCE_SELECTION_MANDATORYFILTER**|  
|**GROUPING_BEHAVIOR**|**DBTYPE_I2**|列舉，指定此階層的預期用戶端分組行為。 可能的值如下：<br /><br /> **EncourageGrouping** (1)<br /><br /> **DiscourageGrouping** (2)|  
|**STRUCTURE_TYPE**|**DBTYPE_WSTR**|表示階層的類型。 有效值包括下列各值：<br /><br /> **自然**<br /><br /> **比較不自然**<br /><br /> **Unknown**|  
  
 排序資料列集**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **DIMENSION_UNIQUE_NAME**， **HIERARCHY_名稱**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_HIERARCHIES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_ORIGIN**|**DBTYPE_UI2**|(選擇性) 預設限制會在 MD_USER_DEFINED 和 MD_SYSTEM_ENABLED 上生效。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION (維度)|  
|**HIERARCHY_VISIBILITY**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 可見<br /><br /> 2 不可見|  
  
## <a name="see-also"></a>請參閱＜  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
