---
title: ObjectStateEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a8d7ba4da1908d2434049c8a71039a259bab8ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定物件是否為開啟或關閉、 連接到執行命令，或擷取資料的資料來源。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指出物件已關閉。|  
|**adStateOpen**|1|指出物件開啟。|  
|**adStateConnecting**|2|表示正在連接物件。|  
|**adStateExecuting**|4|表示物件正在執行命令。|  
|**adStateFetching**|8|指出，正在抓取物件的資料列。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[State 屬性 (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[State 屬性 (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
