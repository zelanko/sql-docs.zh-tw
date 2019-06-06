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
manager: jroth
ms.openlocfilehash: 7345f75d43d302c71db91aefa9097a4d34e72d94
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700962"
---
# <a name="determining-edit-mode"></a>判斷編輯模式
ADO 會維護一個編輯與目前記錄相關聯的緩衝區。 **EditMode**屬性會指出是否已變更到這個緩衝區，或是否會建立新的記錄。 使用**EditMode**來判斷目前的資料錄的編輯狀態。 您可以測試暫止的變更如果編輯程序已中斷，並判斷是否需要使用**更新**或是**CancelUpdate**方法。  
  
 **EditMode**傳回的其中一個**EditModeEnum**詳列於下表的常數。  
  
|常數|描述|  
|--------------|-----------------|  
|**adEditNone**|表示未編輯的作業正在進行中。|  
|**adEditInProgress**|指出目前記錄中的資料已修改但尚未儲存。|  
|**adEditAdd**|指出**AddNew**呼叫的方法，並複製緩衝區中目前的記錄會成為新的記錄尚未儲存到資料庫。|  
|**adEditDelete**|指出目前資料錄已被刪除。|  
  
 **EditMode**可以傳回有效的值，只有當目前的記錄。 **EditMode**會傳回錯誤，如果**BOF**或是**EOF**是**True**或已刪除目前的記錄時。
