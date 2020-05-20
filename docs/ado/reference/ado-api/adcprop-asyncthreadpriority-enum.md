---
title: ADCPROP_ASYNCTHREADPRIORITY_ENUM |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM
helpviewer_keywords:
- ADCPROP_ASYNCTHREADPRIORITY_ENUM [ADO]
ms.assetid: f0965617-17d8-41e0-98d0-f824274735a6
author: rothja
ms.author: jroth
ms.openlocfilehash: ecdc80a2f1e1ace36170a9b4527ba01f0b02ee11
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760654"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
對於 RDS[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，指定抓取資料之非同步執行緒的執行優先權。  
  
 使用這些常數搭配**記錄集**「**背景執行緒優先順序**」動態屬性，這會在 ADO 對 OLE DB 動態屬性索引中參考，並記載于[適用于 OLE DB 檔的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)中。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|設定 [一般] 和 [最高] 之間的優先順序。|  
|**adPriorityBelowNormal**|2|設定 [最低] 和 [一般] 之間的優先順序。|  
|**adPriorityHighest**|5|將優先順序設定為最高的可能。|  
|**AdPriorityLowest**|1|將優先順序設定為最低可能。|  
|**adPriorityNormal**|3|將優先順序設定為 [一般]。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. AdcPropAsyncThreadPriority. ABOVENORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. BELOWNORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. 最高|  
|AdoEnums. AdcPropAsyncThreadPriority。最低|  
|AdoEnums. AdcPropAsyncThreadPriority. NORMAL|
