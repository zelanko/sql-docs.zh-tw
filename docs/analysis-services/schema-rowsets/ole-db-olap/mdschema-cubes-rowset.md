---
title: MDSCHEMA_CUBES 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDSCHEMA_CUBES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_CUBES rowset
ms.assetid: 5f1b63d4-aa3f-48c6-b866-7ffd91675044
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f56517d3f8a974ae54d08f0dda2c24de5025facb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemacubes-rowset"></a>MDSCHEMA_CUBES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述資料庫內 Cube 的結構。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **MDSCHEMA_CUBES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|資料庫的名稱。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|不支援。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Cube 或維度的名稱。 維度名稱前會加上錢幣符號 ($)。<br /><br /> 注意： 只有伺服器和資料庫管理員具有查看從維度建立 cube 的權限。|  
|**CUBE_TYPE**|**DBTYPE_WSTR**|Cube 的類型。 有效值為：<br /><br /> **CUBE**<br /><br /> **維度**|  
|**CUBE_GUID**|**DBTYPE_GUID**|不支援。|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**|不支援。|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**|上次處理 Cube 的時間。|  
|**SCHEMA_UPDATED_BY**|**DBTYPE_WSTR**|不支援。|  
|**LAST_DATA_UPDATE**|**DBTYPE_DBTIMESTAMP**|上次處理 Cube 的時間。|  
|**DATA_UPDATED_BY**|**DBTYPE_WSTR**|不支援。|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Cube 的易記描述。|  
|**IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|布林值，永遠會傳回 true。|  
|**IS_LINKABLE**|**DBTYPE_BOOL**|布林值，指出 Cube 是否可用於連結的 Cube 中。|  
|**IS_WRITE_ENABLED**|**DBTYPE_BOOL**|布林值，指出 Cube 是否可寫入。|  
|**IS_SQL_ENABLED**|**DBTYPE_BOOL**|布林值，指出是否可在 Cube 上使用 SQL。|  
|**CUBE_CAPTION**|**DBTYPE_WSTR**|Cube 的標題。|  
|**BASE_CUBE_NAME**|**DBTYPE_WSTR**|如果這個 Cube 是檢視方塊，這是來源 Cube 的名稱。|  
|**註解**|**DBTYPE_WSTR**|(選擇性) 一組注意事項 (以 XML 格式表示)。|  
  
 排序資料列集**CATALOG_NAME**， **SCHEMA_NAME**， **CUBE_NAME**。  
  
## <a name="restriction-columns"></a>限制資料行  
 **MDSCHEMA_CUBES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|選擇性。|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|（選擇性）預設限制為 1 的值。 點陣圖，其中一個有效的值：<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION (維度)|  
|**基底 Cube_Name**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
