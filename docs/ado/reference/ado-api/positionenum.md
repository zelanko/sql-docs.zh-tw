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
ms.openlocfilehash: 326fc4f1b9b77c8a4470fedc7d55f2d379aff6f3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442710"
---
# <a name="positionenum"></a>PositionEnum
指定記錄指標在記錄 [集](../../../ado/reference/ado-api/recordset-object-ado.md)內的目前位置。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|指出目前的記錄指標位於 BOF (也就是說， [bof](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 屬性為 **True**) 。|  
|**adPosEOF**|-3|指出目前的記錄指標位於 EOF (也就是說， [eof](../../../ado/reference/ado-api/bof-eof-properties-ado.md) 屬性為 **True**) 。|  
|**adPosUnknown**|-1|指出 **記錄集** 是空的、目前的位置未知，或是提供者不支援 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 或 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) 屬性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)  
    :::column-end:::
    :::column:::
        [AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)  
    :::column-end:::
:::row-end:::
