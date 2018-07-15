---
title: MDSCHEMA_MEMBERS 資料列集 |Microsoft Docs
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
- MDSCHEMA_MEMBERS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEMBERS rowset
ms.assetid: 0b1aada0-67f8-4ef6-81b2-0100b65e0c2f
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d36a065ea73f249ce5c4d9dc37cc047ac864cb84
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280014"
---
# <a name="mdschemamembers-rowset"></a>MDSCHEMA_MEMBERS 資料列集
  描述資料庫內的成員。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `MDSCHEMA_MEMBERS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||此成員所屬的資料庫名稱。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||此成員所屬的結構描述名稱。|  
|`CUBE_NAME`|`DBTYPE_WSTR`||此一成員所屬 Cube 的名稱。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||此一成員所屬維度的唯一名稱。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||此成員所屬階層的唯一名稱。|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||此成員所屬層級的唯一名稱。|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`||成員距根階層的距離。 根層級為零 (0)。|  
|`MEMBER_ORDINAL`|`DBTYPE_UI4`||(已被取代) 永遠傳回 `0`。|  
|`MEMBER_NAME`|`DBTYPE_WSTR`||成員的名稱。|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||成員的唯一名稱。|  
|`MEMBER_TYPE`|`DBTYPE_I4`||成員的類型：<br /><br /> -   `MDMEMBER_TYPE_REGULAR` (`1`)<br />-   `MDMEMBER_TYPE_ALL` (`2`)<br />-   `MDMEMBER_TYPE_MEASURE` (`3`)<br />-   `MDMEMBER_TYPE_FORMULA` (`4`)<br />-   `MDMEMBER_TYPE_UNKNOWN` (`0`)<br />-   `MDMEMBER_TYPE_FORMULA` 會優先於`MDMEMBER_TYPE_MEASURE`。 例如，如果 Measures 維度有一個公式 (導出) 成員，會將該成員列為 `MDMEMBER_TYPE_FORMULA`。|  
|`MEMBER_GUID`|`DBTYPE_GUID`||成員的 GUID。 如果 GUID 不存在，則為 `NULL`。|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`||與該成員關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在，就會傳回 `MEMBER_NAME`。|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||成員擁有的子系數目。 這可能只是一個估計值，因此取用者不應該依賴此值做為確實計數。 提供者應會傳回最佳的可能估計值。|  
|`PARENT_LEVEL`|`DBTYPE_UI4`||成員的父系距階層之根層級的距離。 根層級為零 (0)。|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||成員之父系的唯一名稱。 如果是根層級的任何成員，則會傳回 `NULL`。|  
|`PARENT_COUNT`|`DBTYPE_UI4`||此成員擁有的父系數目。|  
|`DESCRIPTION`|`DBTYPE_WSTR`||此資料行一律會傳回 `NULL` 值。<br /><br /> 這個資料行是為了回溯相容性而存在|  
|`EXPRESSION`|`DBTYPE_WSTR`||如果成員的類型是 `MDMEMBER_TYPE_FORMULA`，則為計算的運算式。|  
|`MEMBER_KEY`|`DBTYPE_WSTR`||成員的索引鍵資料行值。 如果成員有複合索引鍵，會傳回 `NULL`。|  
|`IS_PLACEHOLDERMEMBER`|`DBTYPE_BOOL`||布林值，指出成員在維度階層中是否為空位置的預留位置成員。<br /><br /> 只有在 `MDX Compatibility` 屬性已設定為 2 時，才是有效的。|  
|`IS_DATAMEMBER`|`DBTYPE_BOOL`||指出成員是否為資料成員的布林值。<br /><br /> 如果成員是資料成員，則會傳回 True。|  
|`SCOPE`|`DBTYPE_I4`||成員的範圍。 成員可以是工作階段導出成員或是全域導出成員。 資料行會為非導出成員傳回 `NULL`。<br /><br /> 此資料行可以有下列其中一個值：<br /><br /> -MDMEMBER_SCOPE_GLOBAL = 1<br />-MDMEMBER_SCOPE_SESSION = 2|  
|`Zero or more additional columns`|`DBTYPE_UI2`||如果可以從多個層級傳回成員，就不會傳回屬性。 例如，如果非父子式階層的 Tree 運算子是 `PARENT` 與 `SELF`，則不會傳回成員屬性。<br /><br /> 這適用於不完全階層，在這些階層中，三個運算子可從不同的層級傳回成員 (例如，如果之前的層級包含窺視孔，則會要求成員上的父系)。|  
  
 資料列集會在 `CATALOG_NAME`, `SCHEMA_NAME`、`CUBE_NAME`、`DIMENSION_UNIQUE_NAME`、`HIERARCHY_UNIQUE_NAME`、`LEVEL_UNIQUE_NAME`、`LEVEL_NUMBER`、`MEMBER_ORDINAL` 排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 在下表列出的資料行上可能會限制 `MDSCHEMA_MEMBERS` 資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`|選擇性。|  
|`MEMBER_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|選擇性。|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`|選擇性。|  
|`MEMBER_TYPE`|`DBTYPE_I4`|選擇性。|  
|`TREE_OP`|`DBTYPE_I4`|(選擇性) 只適用於單一成員：<br /><br /> -   `MDTREEOP_ANCESTORS` (`0x20`) 會傳回所有上階。<br />-   `MDTREEOP_CHILDREN` (`0x01`) 傳回的直接子系。<br />-   `MDTREEOP_SIBLINGS` (`0x02`) 傳回相同的層級的成員。<br />-   `MDTREEOP_PARENT` (`0x04`) 傳回直屬父代。<br />-   `MDTREEOP_SELF` (`0x08`) 傳回本身傳回的資料列的清單中。<br />-   `MDTREEOP_DESCENDANTS` (`0x10`) 會傳回所有子系。|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(選擇性) 具有下列其中一個有效值的點陣圖：<br /><br /> -1 的 CUBE<br />-2 的維度<br /><br /> 預設限制為值 1。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](ole-db-for-olap-schema-rowsets.md)  
  
  
