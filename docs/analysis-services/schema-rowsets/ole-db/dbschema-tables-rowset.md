---
title: "DBSCHEMA_TABLES 資料列集 |Microsoft 文件"
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
apiname:
- DBSCHEMA_TABLES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1bc193f33395521c62e1b5e998c2098721313d9b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbschematables-rowset"></a>DBSCHEMA_TABLES 資料列集
  識別的量值群組和維度內公開為資料表[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DBSCHEMA_TABLES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG 排列**|**DBTYPE_WSTR**|255|這個物件所屬之目錄的名稱。|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|255|此物件所屬 Cube 的名稱。|  
|**TABLE_NAME**|**DBTYPE_WSTR**|255|物件的名稱，如果**TABLE_TYPE**是**資料表**。|  
|**TABLE_TYPE**|**DBTYPE_WSTR**||資料表的類型。<br /><br /> **資料表**指出物件是量值群組。<br /><br /> **系統資料表**指出物件是維度。|  
|**TABLE_GUID**|**DBTYPE_GUID**||不支援。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||物件的可讀取描述。|  
|**TABLE_PROPID**|**DBTYPE_UI4**||不支援。|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||不支援。|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||上次修改物件的日期。|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**||物件的 OLAP 類型。<br /><br /> **MEASURE_GROUP**指出物件是量值群組。<br /><br /> **CUBE_DIMENSION**指出物件是維度。|  
  
 排序資料列集**TABLE_TYPE**， **table_catalog 排列**， **TABLE_SCHEMA**，和**TABLE_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DBSCHEMA_TABLES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG 排列**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_NAME**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_TYPE**|**DBTYPE_WSTR**|選擇性|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  

