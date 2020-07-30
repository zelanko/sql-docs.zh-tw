---
title: ParameterDirectionEnum |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c109ea1c44fc44a4cdbb585e2c612ebf8c9b2909
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242604"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定[參數](../../../ado/reference/ado-api/parameter-object.md)是否代表輸入參數、輸出參數、輸入和輸出參數，或預存程式的傳回值。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|預設值。 表示參數代表輸入參數。|  
|**adParamInputOutput**|3|表示參數同時代表輸入和輸出參數。|  
|**adParamOutput**|2|表示參數表示輸出參數。|  
|**adParamReturnValue**|4|表示參數代表傳回值。|  
|**adParamUnknown**|0|指出參數方向不明。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.ParameterDirection.INPUT|  
|AdoEnums.ParameterDirection.INPUTOUTPUT|  
|AdoEnums.ParameterDirection.OUTPUT|  
|AdoEnums.ParameterDirection.RETURNVALUE|  
|AdoEnums.ParameterDirection.UNKNOWN|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [CreateParameter 方法 (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [Direction 屬性](../../../ado/reference/ado-api/direction-property.md)  
    :::column-end:::
:::row-end:::
