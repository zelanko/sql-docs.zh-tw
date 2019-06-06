---
title: ParameterDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3f62d2119764466cabb542d26849712d733453ba
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66703262"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定是否[參數](../../../ado/reference/ado-api/parameter-object.md)代表輸入的參數、 輸出參數、 既是輸入和一個 output 參數或從預存程序的傳回值。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|預設值。 指出該參數代表輸入的參數。|  
|**adParamInputOutput**|3|指出該參數代表輸入和輸出的參數。|  
|**adParamOutput**|2|指出參數表示輸出參數。|  
|**adParamReturnValue**|4|指出參數代表傳回的值。|  
|**adParamUnknown**|0|表示未知的參數方向。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ParameterDirection.INPUT|  
|AdoEnums.ParameterDirection.INPUTOUTPUT|  
|AdoEnums.ParameterDirection.OUTPUT|  
|AdoEnums.ParameterDirection.RETURNVALUE|  
|AdoEnums.ParameterDirection.UNKNOWN|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|[Direction 屬性](../../../ado/reference/ado-api/direction-property.md)|
