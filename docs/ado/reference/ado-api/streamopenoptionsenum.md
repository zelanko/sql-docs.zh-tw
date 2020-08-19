---
description: StreamOpenOptionsEnum
title: StreamOpenOptionsEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: rothja
ms.author: jroth
ms.openlocfilehash: e2799d52ef8c46092132a36eb2fe4fb92f5d14d4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441820"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
指定開啟 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件的選項。 這些值可以與 OR 運算合併。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|以非同步模式開啟 **資料流程** 物件。|  
|**adOpenStreamFromRecord**|4|將 *來源* 參數的內容識別為已經開啟的 [記錄](../../../ado/reference/ado-api/record-object-ado.md) 物件。 預設行為是將 *來源* 視為直接指向樹狀結構中節點的 URL。 會開啟與該節點相關聯的預設資料流程。|  
|**adOpenStreamUnspecified**|-1|預設值。 指定以預設選項開啟 **資料流程** 物件。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)
