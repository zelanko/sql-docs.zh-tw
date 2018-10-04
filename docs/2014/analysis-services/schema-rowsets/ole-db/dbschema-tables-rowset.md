---
title: DBSCHEMA_TABLES 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DBSCHEMA_TABLES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 66780a650e3187f3ec62831fd2badf331a1fca4d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153158"
---
# <a name="dbschematables-rowset"></a>DBSCHEMA_TABLES 資料列集
  識別的量值群組和維度內公開為資料表[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DBSCHEMA_TABLES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|255|這個物件所屬之目錄的名稱。|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|255|此物件所屬 Cube 的名稱。|  
|`TABLE_NAME`|`DBTYPE_WSTR`|255|如果 `TABLE_TYPE` 為 `TABLE`，則此為物件的名稱。|  
|`TABLE_TYPE`|`DBTYPE_WSTR`||資料表的類型。<br /><br /> `TABLE` 表示物件是量值群組。<br /><br /> `SYSTEM TABLE` 指出物件是維度。|  
|`TABLE_GUID`|`DBTYPE_GUID`||不支援。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||物件的可讀取描述。|  
|`TABLE_PROPID`|`DBTYPE_UI4`||不支援。|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||不支援。|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||上次修改物件的日期。|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`||物件的 OLAP 類型。<br /><br /> **MEASURE_GROUP**指出物件是量值群組。<br /><br /> `CUBE_DIMENSION` 指出物件是維度。|  
  
 資料列集會按 `TABLE_TYPE`、`TABLE_CATALOG`、`TABLE_SCHEMA` 和 `TABLE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `DBSCHEMA_TABLES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|選擇性|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|選擇性|  
|`TABLE_NAME`|`DBTYPE_WSTR`|選擇性|  
|`TABLE_TYPE`|`DBTYPE_WSTR`|選擇性|  
|`TABLE_OLAP_TYPE`|`DBTYPE_WSTR`|選擇性|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 結構描述資料列集](ole-db-schema-rowsets.md)  
  
  
