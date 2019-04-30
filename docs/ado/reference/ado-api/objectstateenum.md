---
title: ObjectStateEnum | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 560e95bdafe3f5bbae82b200d8f7db0dcb121911
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217718"
---
# <a name="objectstateenum"></a>ObjectStateEnum
指定物件是否為開啟或關閉、 連接到資料來源，執行命令，或擷取資料。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|指出物件已關閉。|  
|**adStateOpen**|1|指出物件已開啟。|  
|**adStateConnecting**|2|指出物件連接。|  
|**adStateExecuting**|4|表示物件正在執行命令。|  
|**adStateFetching**|8|表示要擷取之物件的資料列的。|  
  
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
