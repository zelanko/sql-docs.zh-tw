---
title: "MDSCHEMA_MEASUREGROUPS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MDSCHEMA_MEASUREGROUPS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_MEASUREGROUPS rowset
ms.assetid: bab1bbd0-421b-4fad-9aee-e6511e0e1f1b
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: aebac1aafd7d49e6b5b5c21343161184ba19da34
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="mdschemameasuregroups-rowset"></a>MDSCHEMA_MEASUREGROUPS 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述資料庫內的量值群組。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_MEASUREGROUPS**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
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
  
## <a name="see-also"></a>請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
