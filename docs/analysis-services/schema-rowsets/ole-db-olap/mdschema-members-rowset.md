---
title: MDSCHEMA_MEMBERS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ffe79581b338941ab4fcd379d7da48ce33028633
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029499"
---
# <a name="mdschemamembers-rowset"></a>MDSCHEMA_MEMBERS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述資料庫內的成員。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_MEMBERS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此成員所屬的資料庫名稱。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||此成員所屬的結構描述名稱。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此一成員所屬 Cube 的名稱。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||此一成員所屬維度的唯一名稱。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||此成員所屬階層的唯一名稱。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||此成員所屬層級的唯一名稱。|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**||成員距根階層的距離。 根層級為零 (0)。|  
|**MEMBER_ORDINAL**|**DBTYPE_UI4**||（已被取代）一律傳回**0**。|  
|**MEMBER_NAME**|**DBTYPE_WSTR**||成員的名稱。|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||成員的唯一名稱。|  
|**MEMBER_TYPE**|**DBTYPE_I4**||成員的類型：<br /><br /> **MDMEMBER_TYPE_UNKNOWN** (**0**)<br /><br /> **MDMEMBER_TYPE_REGULAR** (**1**)<br /><br /> **MDMEMBER_TYPE_ALL** (**2**)<br /><br /> **於 MDMEMBER_TYPE_MEASURE** (**3**)<br /><br /> **MDMEMBER_TYPE_FORMULA** (**4**)<br /><br /> <br /><br /> 請注意， <br />                    **MDMEMBER_TYPE_FORMULA**優先於**於 MDMEMBER_TYPE_MEASURE**。 例如，如果 Measures 維度有公式 （導出） 成員，它顯示為**MDMEMBER_TYPE_FORMULA**。|  
|**MEMBER_GUID**|**DBTYPE_GUID**||成員的 GUID。 **NULL**如果 GUID 不存在。|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**||與該成員關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在， **MEMBER_NAME**傳回。|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||成員擁有的子系數目。 這可能只是一個估計值，因此取用者不應該依賴此值做為確實計數。 提供者應會傳回最佳的可能估計值。|  
|**PARENT_LEVEL**|**DBTYPE_UI4**||成員的父系距階層之根層級的距離。 根層級為零 (0)。|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||成員之父系的唯一名稱。 如果是根層級的任何成員，則會傳回**NULL** 。|  
|**PARENT_COUNT**|**DBTYPE_UI4**||此成員擁有的父系數目。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||此資料行一律會傳回**NULL**值。<br /><br /> 這個資料行是為了回溯相容性而存在|  
|**運算式**|**DBTYPE_WSTR**||如果成員是類型的計算的運算式**MDMEMBER_TYPE_FORMULA**。|  
|**MEMBER_KEY**|**DBTYPE_WSTR**||成員的索引鍵資料行值。 傳回**NULL**如果成員有複合索引鍵。|  
|**IS_PLACEHOLDERMEMBER**|**DBTYPE_BOOL**||布林值，指出成員在維度階層中是否為空位置的預留位置成員。<br /><br /> 它是有效才**MDX 相容性**屬性已設為 2。|  
|**IS_DATAMEMBER**|**DBTYPE_BOOL**||指出成員是否為資料成員的布林值。<br /><br /> 如果成員是資料成員，則會傳回 True。|  
|**範圍**|**DBTYPE_I4**||成員的範圍。 成員可以是工作階段導出成員或是全域導出成員。 資料行會傳回**NULL**非導出成員。 此資料行可以有下列其中一個值：<br /><br /> MDMEMBER_SCOPE_GLOBAL=1<br /><br /> MDMEMBER_SCOPE_SESSION=2|  
|**零或多個其他資料行**|**DBTYPE_UI2**||如果可以從多個層級傳回成員，就不會傳回屬性。 例如，如果 Tree 運算子是**父**和**自助**非父子式階層時，任何成員屬性都會傳回。<br /><br /> 這適用於不完全階層，在這些階層中，三個運算子可從不同的層級傳回成員 (例如，如果之前的層級包含窺視孔，則會要求成員上的父系)。|  
  
 排序資料列集**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**， **DIMENSION_UNIQUE_NAME**， **HIERARCHY_UNIQUE_NAME**， **LEVEL_UNIQUE_NAME**， **LEVEL_NUMBER**， **MEMBER_ORDINAL**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_MEMBERS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|選擇性。|  
|**MEMBER_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**|選擇性。|  
|**MEMBER_TYPE**|**DBTYPE_I4**|選擇性。|  
|**TREE_OP**|**DBTYPE_I4**|(選擇性) 只適用於單一成員：<br /><br /> **MDTREEOP_ANCESTORS** (**0x20**) 會傳回所有上階。<br /><br /> **MDTREEOP_CHILDREN** (**0x01**) 傳回直屬子系。<br /><br /> **MDTREEOP_SIBLINGS** (**0x02**) 在相同層級傳回成員。<br /><br /> **MDTREEOP_PARENT** (**0x04**) 傳回的直屬父代。<br /><br /> **MDTREEOP_SELF** (**0x08**) 傳回本身傳回的資料列的清單中。<br /><br /> **MDTREEOP_DESCENDANTS** (**0x10**) 會傳回所有下階。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，下列有效的值之一：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION (維度)|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
