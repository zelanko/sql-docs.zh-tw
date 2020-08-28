---
description: EventReasonEnum
title: EventReasonEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: b676ee2b8585f2bab467cc9f09580721d06fab0c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973569"
---
# <a name="eventreasonenum"></a>EventReasonEnum
指定造成事件發生的原因。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|作業加入了新的記錄。|  
|**adRsnClose**|9|作業關閉 **記錄集**。|  
|**adRsnDelete**|2|作業刪除了記錄。|  
|**adRsnFirstChange**|11|作業會對記錄進行第一次變更。|  
|**adRsnMove**|10|作業在記錄 **集**內移動了記錄指標。|  
|**adRsnMoveFirst**|12|作業會將記錄指標移到記錄 **集**內的第一筆記錄。|  
|**adRsnMoveLast**|15|作業會將記錄指標移到記錄 **集**內的最後一筆記錄。|  
|**adRsnMoveNext**|13|作業會將記錄指標移到記錄 **集中**的下一筆記錄。|  
|**adRsnMovePrevious**|14|作業會將記錄指標移到記錄 **集**內的前一筆記錄。|  
|**adRsnRequery**|7|作業會重新查詢 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
|**adRsnResynch**|8|作業會將 **記錄集** 重新同步處理至資料庫。|  
|**adRsnUndoAddNew**|5|作業會反轉加入新記錄。|  
|**adRsnUndoDelete**|6|反轉刪除記錄的作業。|  
|**adRsnUndoUpdate**|4|反轉記錄更新的作業。|  
|**adRsnUpdate**|3|作業已更新現有的記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. EventReason。 ADDNEW|  
|AdoEnums. EventReason. 關閉|  
|AdoEnums. EventReason. DELETE|  
|AdoEnums. EventReason. FIRSTCHANGE|  
|AdoEnums. EventReason 移動|  
|AdoEnums. EventReason. MOVEFIRST|  
|AdoEnums. EventReason. MOVELAST|  
|AdoEnums. EventReason MOVENEXT|  
|AdoEnums. EventReason. MOVEPREVIOUS|  
|AdoEnums. EventReason。 REQUERY|  
|AdoEnums. EventReason|  
|AdoEnums. EventReason. UNDOADDNEW|  
|AdoEnums. EventReason. UNDODELETE|  
|AdoEnums. EventReason. UNDOUPDATE|  
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
