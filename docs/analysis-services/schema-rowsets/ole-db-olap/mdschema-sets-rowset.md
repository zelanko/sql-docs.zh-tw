---
title: "MDSCHEMA_SETS 資料列集 |Microsoft 文件"
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
apiname: MDSCHEMA_SETS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1e197a9d26eb5839425166fde987de22637603f8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 資料列集
  描述目前定義於資料庫中的任何集合，包括工作階段範圍集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_SETS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|資料庫的名稱。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不支援。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Cube 的名稱。|  
|**SET_NAME**|**DBTYPE_WSTR**|集合中所指定的名稱**CREATE SET**陳述式。|  
|**範圍**|**DBTYPE_I4**|集合的範圍：<br /><br /> **MDSET_SCOPE_GLOBAL** (**1**)<br /><br /> **MDSET_SCOPE_SESSION** (**2**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|不支援。|  
|**運算式**|**DBTYPE_WSTR**|集合的運算式。|  
|**維度**|**DBTYPE_WSTR**|以逗號分隔的清單，其中列出集合中所包含的階層。|  
|**SET_CAPTION**|**DBTYPE_WSTR**|與集合關聯的標籤或標題。 標籤或標題主要是供顯示之用。|  
|**SET_DISPLAY_FOLDER**|**DBTYPE_WSTR**|識別用戶端應用程式用於顯示集合之顯示資料夾路徑的字串。 資料夾層級的分隔符號是由用戶端應用程式所定義。 工具和用戶端所提供的[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，反斜線 (\\) 為層級分隔符號。 若要提供多個顯示資料夾，請使用分號 （;） 來分隔資料夾。|  
|**SET_EVALUATION_CONTEXT**|**DBTYPE_I4**|集合的內容。 集合可以是靜態的，也可以是動態的。 此資料行可以有下列其中一個值：<br /><br /> MDSET_RESOLUTION_STATIC=1<br /><br /> MDSET_RESOLUTION_DYNAMIC=2|  
  
 排序資料列集**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_SETS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SET_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**範圍**|**DBTYPE_I4**|選擇性。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|選擇性。<br /><br /> 注意： 只有一個階層可以包含在內，而且命名集只會傳回其階層完全符合限制。|  
  
## <a name="see-also"></a>請參閱＜  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
