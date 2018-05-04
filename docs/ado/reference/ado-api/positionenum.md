---
title: PositionEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PositionEnum
helpviewer_keywords:
- PositionEnum enumeration
ms.assetid: e69af0a5-3405-4b72-9c6e-6b188ff746fd
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c44bea1a7294b12992a7f2f76abac932f0921cf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="positionenum"></a>PositionEnum
指定目前位置中的記錄指標[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|表示目前的記錄指標位於 BOF (也就是[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性是**True**)。|  
|**adPosEOF**|-3|表示目前的記錄指標位於 EOF (也就是[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性是**True**)。|  
|**adPosUnknown**|-1|表示**資料錄集**是空的目前的位置是未知，或提供者不支援[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)或[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
