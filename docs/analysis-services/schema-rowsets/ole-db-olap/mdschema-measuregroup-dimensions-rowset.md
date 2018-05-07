---
title: MDSCHEMA_MEASUREGROUP_DIMENSIONS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4be854b72c773300115e49551ceaf0ddc4d7db81
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemameasuregroupdimensions-rowset"></a>MDSCHEMA_MEASUREGROUP_DIMENSIONS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  列舉量值群組的維度。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_MEASUREGROUP_DIMENSIONS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此量值群組所屬目錄的名稱。 **NULL**如果提供者不支援類別目錄。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||不支援。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此量值群組所屬 Cube 的名稱。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||量值群組的名稱。|  
|**MEASUREGROUP_CARDINALITY**|**DBTYPE_WSTR**||量值群組中的量值針對單一維度成員所可能擁有的執行個體數目。 可能的值包括：<br /><br /> **其中一個**<br /><br /> **許多**|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||維度的唯一名稱。|  
|**DIMENSION_CARDINALITY**|**DBTYPE_WSTR**||維度成員針對量值群組量值的單一執行個體所可能擁有的執行個體數目。 可能的值包括：<br /><br /> **其中一個**<br /><br /> **許多**|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**||布林值，指出維度中的階層是否為可見。<br /><br /> 傳回**TRUE**如果維度中的一個或多個階層為可見，否則**FALSE**。|  
|**DIMENSION_IS_FACT_DIMENSION**|**DBTYPE_BOOL**||布林值，指出維度是否為事實維度。<br /><br /> 傳回**TRUE**如果維度是事實維度; 否則**FALSE**。|  
|**DIMENSION_PATH**|**DBTYPE_HCHAPTER**||參考維度的維度清單。|  
|**DIMENSION_GRANULARITY**|**DBTYPE_WSTR**||資料粒度階層的唯一名稱。|  
  
 資料列集支援排序**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **MEASUREGROUP_NAME**， **DIMENSION_UNIQUE_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_MEASUREGROUP_DIMENSIONS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> 1 可見<br /><br /> 2 不可見<br /><br /> 預設限制為值 1。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
