---
title: DISCOVER_INSTANCES 資料列集 |Microsoft 文件
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
ms.openlocfilehash: 39705d4efdcec8ed190bc58e2ac1888b3aeef7fe
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="discoverinstances-rowset"></a>DISCOVER_INSTANCES 資料列集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]描述在伺服器上的執行個體。  
  
## <a name="rowset-columns"></a>資料列集資料行  
 **DISCOVER_INSTANCES**資料列集包含下列資料行。  
  
|資料行名稱|類型指標|長度|描述|  
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
  
## <a name="see-also"></a>請參閱  
 [OLE DB for OLAP 結構描述資料列集](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
