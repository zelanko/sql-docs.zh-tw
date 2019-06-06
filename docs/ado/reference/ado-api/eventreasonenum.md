---
title: EventReasonEnum | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ba7675f5fe0abe02130de3c6bfc905070b24ec10
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697941"
---
# <a name="eventreasonenum"></a>EventReasonEnum
指定造成事件發生的原因。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|作業會加入新的記錄。|  
|**adRsnClose**|9|作業已關閉**資料錄集**。|  
|**adRsnDelete**|2|作業已刪除的記錄。|  
|**adRsnFirstChange**|11|作業會對記錄中的第一項變更。|  
|**adRsnMove**|10|作業移動中的記錄指標**資料錄集**。|  
|**adRsnMoveFirst**|12|作業移到中的第一筆記錄的記錄指標**資料錄集**。|  
|**adRsnMoveLast**|15|作業移到中的最後一個記錄的記錄指標**資料錄集**。|  
|**adRsnMoveNext**|13|作業移至下一筆記錄的記錄指標**資料錄集**。|  
|**adRsnMovePrevious**|14|作業移到在上一筆記錄的記錄指標**資料錄集**。|  
|**adRsnRequery**|7|查詢作業[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
|**adRsnResynch**|8|重新同步處理的作業**資料錄集**與資料庫。|  
|**adRsnUndoAddNew**|5|作業會回復新記錄的新增。|  
|**adRsnUndoDelete**|6|作業會反轉記錄的刪除。|  
|**adRsnUndoUpdate**|4|作業會回復為記錄的更新。|  
|**adRsnUpdate**|3|作業會更新現有的記錄。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.EventReason.ADDNEW|  
|AdoEnums.EventReason.CLOSE|  
|AdoEnums.EventReason.DELETE|  
|AdoEnums.EventReason.FIRSTCHANGE|  
|AdoEnums.EventReason.MOVE|  
|AdoEnums.EventReason.MOVEFIRST|  
|AdoEnums.EventReason.MOVELAST|  
|AdoEnums.EventReason.MOVENEXT|  
|AdoEnums.EventReason.MOVEPREVIOUS|  
|AdoEnums.EventReason.REQUERY|  
|AdoEnums.EventReason.RESYNCH|  
|AdoEnums.EventReason.UNDOADDNEW|  
|AdoEnums.EventReason.UNDODELETE|  
|AdoEnums.EventReason.UNDOUPDATE|  
|AdoEnums.EventReason.UPDATE|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[WillChangeRecord 和 RecordChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[WillMove 和 MoveComplete 事件 (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)||
