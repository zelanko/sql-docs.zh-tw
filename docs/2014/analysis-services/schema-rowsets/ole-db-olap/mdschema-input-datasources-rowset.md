---
title: MDSCHEMA_INPUT_DATASOURCES 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_INPUT_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa2f372c4facb1b2e51561bbd82a8e35fe8ed134
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210028"
---
# <a name="mdschemainputdatasources-rowset"></a>MDSCHEMA_INPUT_DATASOURCES 資料列集
  說明在資料庫內定義的資料來源。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_INPUT_DATASOURCES`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此資料來源所屬目錄的名稱。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||不支援。|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`||資料來源物件的名稱。|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`||資料來源的類型。 有效值包括：<br /><br /> -   `Relational`<br />-   `Olap`|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||建立資料來源的日期。|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||上次修改資料來源的日期和時間。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||動作的易記描述。|  
|`TIMEOUT`|`DBTYPE_UI4`||資料來源的逾時。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_INPUT_DATASOURCES` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  
