---
title: "MDSCHEMA_MEASURES 資料列集 |Microsoft 文件"
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
apiname:
- MDSCHEMA_MEASURES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c77b91b179e360f539549cda05d0a17f0697ee56
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemameasures-rowset"></a>MDSCHEMA_MEASURES 資料列集
  描述 Cube 內的每個量值。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_MEASURES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此量值所屬之目錄的名稱。 **NULL**如果提供者不支援類別目錄。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||此量值所屬之結構描述的名稱。 **NULL**如果提供者不支援結構描述。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此量值所屬 Cube 的名稱。|  
|**MEASURE_NAME**|**DBTYPE_WSTR**||量值的名稱。|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**||量值的唯一名稱。 對於會依識別資格產生唯一名稱的提供者，此名稱的每個元件會使用分隔符號。|  
|**MEASURE_CAPTION**|**DBTYPE_WSTR**||與量值關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在， **MEASURE_NAME**傳回。|  
|**MEASURE_GUID**|**DBTYPE_GUID**||不支援。|  
|**MEASURE_AGGREGATOR**|**DBTYPE_I4**||識別如何衍生量值的列舉。 可以是下列其中一個值：<br /><br /> **MDMEASURE_AGGR_SUM** (**1**) 識別量值彙總從**總和**。<br /><br /> **MDMEASURE_AGGR_COUNT** (**2**) 識別量值彙總從**計數**。<br /><br /> **MDMEASURE_AGGR_MIN** (**3**) 識別量值彙總從**MIN**。<br /><br /> **MDMEASURE_AGGR_MAX** (**4**) 識別量值彙總從**MAX**。<br /><br /> **MDMEASURE_AGGR_AVG** (**5**) 識別量值彙總從**AVG**。<br /><br /> **MDMEASURE_AGGR_VAR** (**6**) 識別量值彙總從**VAR**。<br /><br /> **MDMEASURE_AGGR_STD** (**7**) 識別量值彙總從**STDEV**。<br /><br /> **MDMEASURE_AGGR_DST** (**8**) 識別量值彙總從**相異計數量**。<br /><br /> **MDMEASURE_AGGR_NONE** (**9**) 識別量值彙總從**NONE**。<br /><br /> **MDMEASURE_AGGR_AVGCHILDREN** (**10**) 識別量值彙總從**AVERAGEOFCHILDREN**。<br /><br /> **MDMEASURE_AGGR_FIRSTCHILD** (**11**) 識別量值彙總從**FIRSTCHILD**。<br /><br /> **MDMEASURE_AGGR_LASTCHILD** (**12**) 識別量值彙總從**LASTCHILD**。<br /><br /> **MDMEASURE_AGGR_FIRSTNONEMPTY** (**13**) 識別量值彙總從**FIRSTNONEMPTY**，<br /><br /> **MDMEASURE_AGGR_LASTNONEMPTY** (**14**) 識別量值彙總從**LASTNONEMPTY**。<br /><br /> **MDMEASURE_AGGR_BYACCOUNT** (**15**) 識別量值彙總從**BYACCOUNT**。<br /><br /> **MDMEASURE_AGGR_CALCULATED** (**127**) 識別量值衍生自不是上述任何單一函數的公式。<br /><br /> **MDMEASURE_AGGR_UNKNOWN** (**0**) 識別量值衍生自未知的彙總函式或公式。|  
|**DATA_TYPE**|**DBTYPE_UI2**||量值的資料類型。|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||如果量值物件的資料類型為精確數值，則為屬性的最大有效位數。 **NULL**對於所有其他屬性類型。|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||如果量值物件的類型指標為在小數點右邊的位數**DBTYPE_NUMERIC**或**DBTYPE_DECIMAL**。 否則，這個值是**NULL**。|  
|**MEASURE_UNITS**|**DBTYPE_WSTR**||不支援|  
|**DESCRIPTION**|**DBTYPE_WSTR**||人們可讀取的量值描述。 **NULL**如果沒有描述。|  
|**運算式**|**DBTYPE_WSTR**||成員的運算式。|  
|**MEASURE_IS_VISIBLE**|**DBTYPE_BOOL**||布林值，永遠會傳回 True。 如果量值為不可見，就不會包含在結構描述資料列集中。|  
|**LEVELS_LIST**|**DBTYPE_WSTR**||字串，一律會傳回**NULL**。|  
|**MEASURE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**||SQL 查詢中對應到量值名稱之資料行的名稱。|  
|**MEASURE_UNQUALIFIED_CAPTION**|**DBTYPE_WSTR**||量值的名稱，未使用量值群組名稱限定。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||此量值所屬之量值群組的名稱。|  
|**MEASURE_DISPLAY_FOLDER**|**DBTYPE_WSTR**||在使用者介面中顯示量值時所使用的路徑。 資料夾名稱將以分號分隔。 巢狀的資料夾會以反斜線 (\\)。|  
|**DEFAULT_FORMAT_STRING**|**DBTYPE_WSTR**||量值的預設格式字串。|  
  
 排序資料列集**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **MEASURE_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_MEASURES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASURE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION (維度)|  
|**MEASURE_VISIBILITY**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 可見<br /><br /> 2 不可見|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

