---
description: PositionEnum
title: PositionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a871f6d2f7b73e7430761318a5acee31f05df3c1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990069"
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