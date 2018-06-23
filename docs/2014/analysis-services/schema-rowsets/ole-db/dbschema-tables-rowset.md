---
title: DBSCHEMA_TABLES 資料列集 |Microsoft 文件
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
- DBSCHEMA_TABLES
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_TABLES rowset
ms.assetid: 14c16e6b-0aff-4ad1-b98f-cdb7df0f8d73
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9033dc2f48b74bc13268d06f66a084f4ada22cfc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037766"
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
  
  