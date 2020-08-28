---
description: ParameterDirectionEnum
title: ParameterDirectionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: b7422bf0037adc8d756c20c82404a7f3b06ae9e3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990129"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定 [參數](./parameter-object.md) 是否代表輸入參數、輸出參數、輸入和輸出參數，或預存程式的傳回值。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|預設值。 指出參數表示輸入參數。|  
|**adParamInputOutput**|3|指出參數同時代表輸入和輸出參數。|  
|**adParamOutput**|2|指出參數代表輸出參數。|  
|**adParamReturnValue**|4|指出參數代表傳回值。|  
|**adParamUnknown**|0|指出參數方向未知。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
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
        [CreateParameter 方法 (ADO)](./createparameter-method-ado.md)  
    :::column-end:::
    :::column:::
        [Direction 屬性](./direction-property.md)  
    :::column-end:::
:::row-end:::