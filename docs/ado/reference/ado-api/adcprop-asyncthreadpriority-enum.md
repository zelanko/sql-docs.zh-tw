---
description: ADCPROP_ASYNCTHREADPRIORITY_ENUM
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
ms.openlocfilehash: 00878f5caddcbd8060c9c85222bc061533542bf8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451620"
---
# <a name="adcprop_asyncthreadpriority_enum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
針對 RDS [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件，指定抓取資料之非同步執行緒的執行優先權。  
  
 使用這些常數搭配 **記錄集** 「**背景執行緒優先順序**」動態屬性，它會在 ADO 對 OLE DB 動態屬性索引中參考，並記載于適用于 [OLE DB 檔的 Microsoft 資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 中。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|設定 [一般] 和 [最高] 之間的優先順序。|  
|**adPriorityBelowNormal**|2|設定最低和一般之間的優先順序。|  
|**adPriorityHighest**|5|將優先權設定為最高的可能。|  
|**AdPriorityLowest**|1|將優先權設定為最低可能。|  
|**adPriorityNormal**|3|將優先權設定為 normal。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums. AdcPropAsyncThreadPriority. ABOVENORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority. BELOWNORMAL|  
|AdoEnums. AdcPropAsyncThreadPriority （最高）|  
|AdoEnums. AdcPropAsyncThreadPriority|  
|AdoEnums. AdcPropAsyncThreadPriority. NORMAL|
