---
title: MDSCHEMA_MEASUREGROUPS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: df2bfe8aecc32c8f046d18fff4e72cd15409fdc8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029039"
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述資料庫內的量值群組。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_MEASUREGROUPS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||此量值群組所屬目錄的名稱。 **NULL**如果提供者不支援類別目錄。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||不支援。|  
|**CUBE_NAME**|**DBTYPE_WSTR**||此量值群組所屬 Cube 的名稱。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||量值群組的名稱。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||成員的可讀取描述。|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**||布林值，指出量值群組是否為可寫入。<br /><br /> 傳回**true**如果量值群組啟用寫入。|  
|**MEASUREGROUP_CAPTION**|**DBTYPE_WSTR**||量值群組的顯示標題。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_MEASUREGROUPS**上表中的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
