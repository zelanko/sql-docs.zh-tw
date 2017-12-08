---
title: "DBSCHEMA_CATALOGS 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DBSCHEMA_CATALOGS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6e001700aab7f231e186576226ae97468572698d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="dbschemacatalogs-rowset"></a>DBSCHEMA_CATALOGS 資料列集
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
  
## <a name="see-also"></a>請參閱＜  
 [OLE DB 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
