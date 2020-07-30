---
title: ObjectStateEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: rothja
ms.author: jroth
ms.openlocfilehash: e0b69deb64cc4ea04c007fd3d3328cb4154cc3e8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242615"
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定物件為開啟或關閉、連接至資料來源、執行命令，或抓取資料。  
  
|持續性|值|說明|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指出物件已關閉。|  
|**adStateOpen**|1|指出物件已開啟。|  
|**adStateConnecting**|2|指出物件正在連接。|  
|**adStateExecuting**|4|指出物件正在執行命令。|  
|**adStateFetching**|8|表示正在抓取物件的資料列。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|||

:::row:::
    :::column:::
        [State 屬性 (ADO)](../../../ado/reference/ado-api/state-property-ado.md)  
    :::column-end:::
    :::column:::
        [State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)  
    :::column-end:::
:::row-end:::
