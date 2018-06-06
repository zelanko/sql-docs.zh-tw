---
title: DBSCHEMA_CATALOGS 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 61e4de1591752919a5916d6044591bda49b14992
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="dbschemacatalogs-rowset"></a>DBSCHEMA_CATALOGS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別與可從資料庫管理系統 (DBMS) 存取之目錄相關聯的實體屬性 (Attribute)。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DBSCHEMA_CATALOGS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|255|目錄的名稱。 不可為 null。|  
|**DESCRIPTION**|**DBTYPE_WSTR**||資料表的可讀取描述。|  
|**角色**|**DBTYPE_WSTR**||目前使用者所屬角色的以逗號分隔的清單。<br /><br /> 星號 (\*) 是包含為角色，如果目前的使用者是伺服器或資料庫管理員。<br /><br /> **使用者名稱**附加至**角色**如果其中一個角色使用動態安全性。|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||上次修改目錄的日期。|  
  
 排序資料列集**CATALOG_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DBSCHEMA_CATALOGS**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
