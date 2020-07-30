---
title: StreamReadEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: rothja
ms.author: jroth
ms.openlocfilehash: 92c599665548c36b8349290b02d197393f707fbf
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243189"
---
# <a name="streamreadenum"></a>StreamReadEnum
指定是否應從[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件讀取整個資料流程或下一行。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|預設值。 從資料流程讀取所有位元組，從目前位置到[eos](../../../ado/reference/ado-api/eos-property.md)標記為止。 這是唯一具有二進位資料流程（[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeBinary**）的有效**StreamReadEnum**值。|  
|**adReadLine**|-2|從資料流程讀取下一行（由[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)屬性指定）。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Read 方法](../../../ado/reference/ado-api/read-method.md)  
    :::column-end:::
    :::column:::
        [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)  
    :::column-end:::
:::row-end:::
