---
title: MDSCHEMA_MEASUREGROUPS 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_MEASUREGROUPS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7846fa9eb88a91a945c787cfec0fe19d0c520cf6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300978"
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 資料列集
  描述資料庫內的量值群組。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_MEASUREGROUPS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此量值群組所屬目錄的名稱。 如果提供者不支援目錄，則為 `NULL`。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此量值群組所屬 Cube 的名稱。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||量值群組的名稱。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||成員的可讀取描述。|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||布林值，指出量值群組是否為可寫入。<br /><br /> 如果量值群組為可寫入，則傳回 `true`。|  
|`MEASUREGROUP_CAPTION`|`DBTYPE_WSTR`||量值群組的顯示標題。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 下表中的資料行上可以限制 `MDSCHEMA_MEASUREGROUPS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  
