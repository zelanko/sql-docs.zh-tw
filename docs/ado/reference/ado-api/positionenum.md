---
description: PositionEnum
title: PositionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d7b443e94f3bea5977aeaf953e84c66c826daeb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773167"
---
# <a name="positionenum"></a>PositionEnum
指定記錄指標在記錄 [集](./recordset-object-ado.md)內的目前位置。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|指出目前的記錄指標位於 BOF (也就是說， [bof](./bof-eof-properties-ado.md) 屬性為 **True**) 。|  
|**adPosEOF**|-3|指出目前的記錄指標位於 EOF (也就是說， [eof](./bof-eof-properties-ado.md) 屬性為 **True**) 。|  
|**adPosUnknown**|-1|指出 **記錄集** 是空的、目前的位置未知，或是提供者不支援 [AbsolutePage](./absolutepage-property-ado.md) 或 [AbsolutePosition](./absoluteposition-property-ado.md) 屬性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [AbsolutePage 屬性 (ADO)](./absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [AbsolutePosition 屬性 (ADO)](./absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::