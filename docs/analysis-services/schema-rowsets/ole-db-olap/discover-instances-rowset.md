---
title: "DISCOVER_INSTANCES 資料列集 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
apiname:
- DISCOVER_INSTANCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbed6de71f83da959591003039fe5910a1a4c53d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 資料列集
  描述伺服器上的執行個體。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_INSTANCES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**執行個體名稱**|**DBTYPE_WSTR**||執行個體的名稱。|  
|**INSTANCE_PORT_NUMBER**|**DBTYPE_I4**||執行個體所接聽的通訊埠編號。|  
|**INSTANCE_STATE**|**DBTYPE_I4**||伺服器執行個體的狀態：<br /><br /> **啟動**<br /><br /> **Stopped**<br /><br /> **啟動**<br /><br /> **停止**<br /><br /> **已暫停**|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="restriction-columns"></a>限制資料行  
 **DISCOVER_INSTANCES**上表中列出的資料行可能會限制資料列集。  
  
|資料行名稱|類型指標|限制狀態|  
|-----------------|--------------------|-----------------------|  
|**執行個體名稱**|**DBTYPE_WSTR**|選擇性。|  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

