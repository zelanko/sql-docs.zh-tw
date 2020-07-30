---
title: EventReasonEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: rothja
ms.author: jroth
ms.openlocfilehash: 94b36cbab5ffe7c22f4d1941e61af8fabc8b9973
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242728"
---
# <a name="eventreasonenum"></a>EventReasonEnum
指定造成事件發生的原因。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|作業已加入新的記錄。|  
|**adRsnClose**|9|作業已關閉**記錄集**。|  
|**adRsnDelete**|2|作業已刪除記錄。|  
|**adRsnFirstChange**|11|作業進行第一次的記錄變更。|  
|**adRsnMove**|10|作業會將記錄指標移動到**記錄集**內。|  
|**adRsnMoveFirst**|12|作業會將記錄指標移至記錄**集**內的第一筆記錄。|  
|**adRsnMoveLast**|15|作業會將記錄指標移至記錄**集**內的最後一個記錄。|  
|**adRsnMoveNext**|13|作業會將記錄指標移至記錄**集**內的下一個記錄。|  
|**adRsnMovePrevious**|14|作業會將記錄指標移至記錄**集**內的上一個記錄。|  
|**adRsnRequery**|7|作業會重新查詢[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
|**adRsnResynch**|8|作業會將**記錄集**與資料庫重新同步處理。|  
|**adRsnUndoAddNew**|5|作業已反轉加入新記錄。|  
|**adRsnUndoDelete**|6|作業反轉刪除記錄。|  
|**adRsnUndoUpdate**|4|作業反轉記錄的更新。|  
|**adRsnUpdate**|3|作業已更新現有的記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. EventReason. ADDNEW|  
|AdoEnums. EventReason. CLOSE|  
|AdoEnums. EventReason. DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums. EventReason. MOVE|  
|AdoEnums. EventReason. MOVEFIRST|  
|AdoEnums. EventReason. MOVELAST|  
|AdoEnums. EventReason. MOVENEXT|  
|AdoEnums. EventReason. MOVEPREVIOUS|  
|AdoEnums. EventReason. REQUERY|  
|AdoEnums. EventReason. 同步|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums. EventReason. UPDATE|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [WillChangeRecord 和 RecordChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  

        [WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [WillMove 和 MoveComplete 事件 (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
