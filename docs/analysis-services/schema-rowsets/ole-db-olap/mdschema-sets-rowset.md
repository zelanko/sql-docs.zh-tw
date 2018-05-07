---
title: MDSCHEMA_SETS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e3750594327d247cbb9f8abbc577c29027d1c92f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
