---
title: ParameterDirectionEnum |Microsoft 文件
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
- ParameterDirectionEnum
helpviewer_keywords:
- ParameterDirectionEnum enumeration [ADO]
ms.assetid: c66aa6e6-d4f0-4f0f-9640-e08ae6cfdef3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92304ffbec64534e1099f04ff5915a2b1c31cea3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定是否[參數](../../../ado/reference/ado-api/parameter-object.md)代表輸入的參數、 輸出參數、 既是輸入和輸出參數或從預存程序傳回的值。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|預設值。 指出此參數代表的輸入的參數。|  
|**adParamInputOutput**|3|指出此參數代表輸入和輸出的參數。|  
|**adParamOutput**|2|指出此參數代表輸出參數。|  
|**adParamReturnValue**|4|指出此參數代表傳回的值。|  
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
