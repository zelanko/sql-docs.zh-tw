---
title: MDSCHEMA_SETS 資料列集 |Microsoft 文件
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
- MDSCHEMA_SETS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: edc33b87256fb680225eaaa087ff655be1b82851
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146199"
---
# <a name="mdschemasets-rowset"></a>MDSCHEMA_SETS 資料列集
  描述目前定義於資料庫中的任何集合，包括工作階段範圍集。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_SETS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||資料庫的名稱。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Cube 的名稱。|  
|`SET_NAME`|`DBTYPE_WSTR`||`CREATE SET` 陳述式中指定的集合名稱。|  
|`SCOPE`|`DBTYPE_I4`||集合的範圍：<br /><br /> -   `MDSET_SCOPE_GLOBAL` (`1`)<br />-   `MDSET_SCOPE_SESSION` (`2`)|  
|`DESCRIPTION`|`DBTYPE_WSTR`||不支援。|  
|`EXPRESSION`|`DBTYPE_WSTR`||集合的運算式。|  
|`DIMENSIONS`|`DBTYPE_WSTR`||以逗號分隔的清單，其中列出集合中所包含的階層。|  
|`SET_CAPTION`|`DBTYPE_WSTR`||與集合關聯的標籤或標題。 標籤或標題主要是供顯示之用。|  
|`SET_DISPLAY_FOLDER`|`DBTYPE_WSTR`||識別用戶端應用程式用於顯示集合之顯示資料夾路徑的字串。 資料夾層級的分隔符號是由用戶端應用程式所定義。 工具和用戶端所提供的[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，反斜線 (\\) 為層級分隔符號。 若要提供多個顯示資料夾，請使用分號 （;） 來分隔資料夾。|  
|`SET_EVALUATION_CONTEXT`|`DBTYPE_I4`||集合的內容。 集合可以是靜態的，也可以是動態的。<br /><br /> 此資料行可以有下列其中一個值：<br /><br /> -MDSET_RESOLUTION_STATIC = 1<br />-MDSET_RESOLUTION_DYNAMIC = 2|  
  
 資料列集會在 `CATALOG_NAME`、`SCHEMA_NAME` 和 `CUBE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_SETS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SET_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCOPE`|`DBTYPE_I4`|選擇性。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|選擇性。 **注意：** 只能有一個階層可以包含在內，而且命名集只會傳回其階層完全符合限制。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  