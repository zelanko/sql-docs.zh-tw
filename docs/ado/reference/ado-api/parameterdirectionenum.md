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
ms.openlocfilehash: 8c586b4e7ce2e18411d147e8aafb4eb144e01e6f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442780"
---
# <a name="parameterdirectionenum"></a>ParameterDirectionEnum
指定 [參數](../../../ado/reference/ado-api/parameter-object.md) 是否代表輸入參數、輸出參數、輸入和輸出參數，或預存程式的傳回值。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adParamInput**|1|預設值。 指出參數表示輸入參數。|  
|**adParamInputOutput**|3|指出參數同時代表輸入和輸出參數。|  
|**adParamOutput**|2|指出參數代表輸出參數。|  
|**adParamReturnValue**|4|指出參數代表傳回值。|  
|**adParamUnknown**|0|指出參數方向未知。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
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
