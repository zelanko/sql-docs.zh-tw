---
title: 判斷編輯模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22e63bad49586bbbc1a5616114055779cd3ea041
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925540"
---
# <a name="determining-edit-mode"></a>判斷編輯模式
ADO 會維護與目前記錄相關聯的編輯緩衝區。 **EditMode**屬性會指出是否已對此緩衝區進行變更，或是否已建立新的記錄。 使用**EditMode**來判斷目前記錄的編輯狀態。 如果編輯進程已中斷，您可以測試暫止的變更，並判斷您是否需要使用**Update**或**CancelUpdate**方法。  
  
 **EditMode**會傳回下表所列的其中一個**EditModeEnum**常數。  
  
|持續性|描述|  
|--------------|-----------------|  
|**adEditNone**|表示沒有正在進行的編輯作業。|  
|**adEditInProgress**|指出目前記錄中的資料已修改但未儲存。|  
|**adEditAdd**|表示已呼叫**AddNew**方法，而且複製緩衝區中的目前記錄是尚未儲存到資料庫的新記錄。|  
|**adEditDelete**|指出目前的記錄已刪除。|  
  
 只有在目前的記錄時， **EditMode**才會傳回有效的值。 如果**BOF**或**EOF**為**True** ，或目前的記錄已刪除，則**EditMode**會傳回錯誤。
