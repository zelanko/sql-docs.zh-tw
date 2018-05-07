---
title: DISCOVER_INSTANCES 資料列集 |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4143aa33cc4c09914ffb05aaccbb12f2fe64d440
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
