---
description: ParameterDirectionEnum
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
ms.openlocfilehash: cdd0e393c7fc5214866142150c7ff497e48e7122
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773327"
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