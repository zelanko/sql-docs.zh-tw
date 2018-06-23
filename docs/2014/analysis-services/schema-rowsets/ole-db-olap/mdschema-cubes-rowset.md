---
title: MDSCHEMA_CUBES 資料列集 |Microsoft 文件
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
- MDSCHEMA_CUBES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 0044c9943b2f2819ea216c735f298b7e30de7a3a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134710"
---
# <a name="mdschemacubes-rowset"></a>MDSCHEMA_CUBES 資料列集
  描述資料庫內 Cube 的結構。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_CUBES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||資料庫的名稱。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Cube 或維度的名稱。 維度名稱前會加上錢幣符號 ($)。 **注意：** 只有伺服器和資料庫管理員具有查看從維度建立 cube 的權限。|  
|`CUBE_TYPE`|`DBTYPE_WSTR`||Cube 的類型。 有效值為：<br /><br /> -   `CUBE`<br />-   `DIMENSION`|  
|`CUBE_GUID`|`DBTYPE_GUID`||不支援。|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||不支援。|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||上次處理 Cube 的時間。|  
|`SCHEMA_UPDATED_BY`|`DBTYPE_WSTR`||不支援。|  
|`LAST_DATA_UPDATE`|`DBTYPE_DBTIMESTAMP`||上次處理 Cube 的時間。|  
|`DATA_UPDATED_BY`|`DBTYPE_WSTR`||不支援。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Cube 的易記描述。|  
|`IS_DRILLTHROUGH_ENABLED`|`DBTYPE_BOOL`||布林值，永遠會傳回 true。|  
|`IS_LINKABLE`|`DBTYPE_BOOL`||布林值，指出 Cube 是否可用於連結的 Cube 中。|  
|`IS_WRITE_ENABLED`|`DBTYPE_BOOL`||布林值，指出 Cube 是否可寫入。|  
|`IS_SQL_ENABLED`|`DBTYPE_BOOL`||布林值，指出是否可在 Cube 上使用 SQL。|  
|`CUBE_CAPTION`|`DBTYPE_WSTR`||Cube 的標題。|  
|`BASE_CUBE_NAME`|`DBTYPE_WSTR`||如果這個 Cube 是檢視方塊，這是來源 Cube 的名稱。|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||(選擇性) 一組注意事項 (以 XML 格式表示)。|  
  
 資料列集會在 `CATALOG_NAME`、`SCHEMA_NAME` 和 `CUBE_NAME` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_CUBES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 的 CUBE<br />-2 的維度<br /><br /> 預設限制為值 1。|  
|`Base Cube_Name`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  