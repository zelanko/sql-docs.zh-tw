---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d5f7ca47177a953313ff983bb25f9178b73b4930
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917599"
---
# <a name="positionenum"></a>PositionEnum
指定記錄指標在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)內的目前位置。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPosBOF**|-2|指出目前的記錄指標位於 BOF （也就是[bof](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性為**True**）。|  
|**adPosEOF**|-3|指出目前的記錄指標位於 EOF （也就是[eof](../../../ado/reference/ado-api/bof-eof-properties-ado.md)屬性為**True**）。|  
|**adPosUnknown**|-1|指出**記錄集**是空的、目前的位置不明，或提供者不支援[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)或[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.Position.BOF|  
|AdoEnums.Position.EOF|  
|AdoEnums.Position.UNKNOWN|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)|[AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|
