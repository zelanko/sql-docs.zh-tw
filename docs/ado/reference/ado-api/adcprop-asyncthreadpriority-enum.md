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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0b9d4e0e6f844ef2dda18e95aadfcf3b910995d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824646"
---
# <a name="adcpropasyncthreadpriorityenum"></a>ADCPROP_ASYNCTHREADPRIORITY_ENUM
對於使用 RDS[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件時，指定擷取資料的非同步執行緒的執行優先權。  
  
 使用這些常數**資料錄集**"**背景執行緒優先順序**「 動態屬性，這是參考 ADO-OLE DB 動態屬性索引中，記載於[Microsoft OLE DB 的資料指標服務](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)文件。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPriorityAboveNormal**|4|設定之間正常和最高的優先權。|  
|**adPriorityBelowNormal**|2|最低與一般之間設定優先權。|  
|**adPriorityHighest**|5|設定最高的可能優先權。|  
|**AdPriorityLowest**|1|設定優先順序到最低的可能。|  
|**adPriorityNormal**|3|設定為 normal 的優先權。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.AdcPropAsyncThreadPriority.ABOVENORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.BELOWNORMAL|  
|AdoEnums.AdcPropAsyncThreadPriority.HIGHEST|  
|AdoEnums.AdcPropAsyncThreadPriority.LOWEST|  
|AdoEnums.AdcPropAsyncThreadPriority.NORMAL|
