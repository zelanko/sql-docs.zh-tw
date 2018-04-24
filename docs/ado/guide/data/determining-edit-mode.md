---
title: 判斷編輯模式 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8557d0d514e37491a7d0952afcc14ae60d03d1ae
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="determining-edit-mode"></a>判斷編輯模式
ADO 會維護目前記錄相關聯的編輯緩衝區。 **EditMode**屬性會指出是否已變更到這個緩衝區，或是否會建立新的記錄。 使用**EditMode**來判斷目前記錄的編輯狀態。 您可以測試暫止的變更如果編輯程序已中斷，並判斷是否需要使用**更新**或**CancelUpdate**方法。  
  
 **EditMode**傳回的其中一個**EditModeEnum**下表中列出的常數。  
  
|常數|Description|  
|--------------|-----------------|  
|**adEditNone**|表示未編輯的作業正在進行中。|  
|**adEditInProgress**|指出目前記錄中的資料已修改但尚未儲存。|  
|**adEditAdd**|表示**AddNew**已呼叫方法，並複製緩衝區中目前的記錄是一種新的記錄，不儲存到資料庫。|  
|**adEditDelete**|指出目前的記錄已被刪除。|  
  
 **EditMode**可以傳回有效的值，只有當目前的記錄。 **EditMode**會傳回錯誤，如果**BOF**或**EOF**是**True**或已刪除目前的記錄。
